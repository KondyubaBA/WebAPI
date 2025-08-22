## Порядок установления WebRTC соединения

### 1. Инициализация соединений
#### Peer1:
```js
const pc1 = new RTCPeerConnection({
    iceServers: [
        { urls: 'stun:stun.l.google.com:19302' },
        { urls: 'stun:stun1.l.google.com:19302' }
    ]
});
```

#### Peer2:
```js
const pc2 = new RTCPeerConnection({
    iceServers: [
        { urls: 'stun:stun.l.google.com:19302' },
        { urls: 'stun:stun1.l.google.com:19302' }
    ]
});
```

### 2. Настройка обработчиков ICE кандидатов
#### Peer1:
```js
pc1.onicecandidate = (event) => {
    if (event.candidate) {
        // Отправляем кандидат Peer2 через сервер
        sendToPeer2ViaServer({
            type: 'ice-candidate',
            candidate: event.candidate
        });
    }
};
```

#### Peer2:
```js
pc2.onicecandidate = (event) => {
    if (event.candidate) {
        // Отправляем кандидат Peer1 через сервер
        sendToPeer1ViaServer({
            type: 'ice-candidate',
            candidate: event.candidate
        });
    }
};
```

### 3. Создание и обмен предложением (Offer)
#### Peer1 создает предложение:
```js
async function createOffer() {
    const offer = await pc1.createOffer();
    await pc1.setLocalDescription(offer);
    
    // Отправляем предложение Peer2
    sendToPeer2ViaServer({
        type: 'offer',
        offer: offer
    });
}
```

#### Peer2 получает предложение:
```js
async function handleOffer(offer) {
    await pc2.setRemoteDescription(offer);
    
    // Создаем ответ
    const answer = await pc2.createAnswer();
    await pc2.setLocalDescription(answer);
    
    // Отправляем ответ Peer1
    sendToPeer1ViaServer({
        type: 'answer',
        answer: answer
    });
}
```

### 4. Обработка ответа (Answer)
#### Peer1 получает ответ:
```js
async function handleAnswer(answer) {
    await pc1.setRemoteDescription(answer);
}
```

### 5. Обмен ICE кандидатами
#### Peer1 добавляет кандидат от Peer2:
```js
async function handleIceCandidate(candidate) {
    try {
        await pc1.addIceCandidate(candidate);
    } catch (error) {
        console.error('Ошибка добавления ICE кандидата:', error);
    }
}
```

#### Peer2 добавляет кандидат от Peer1:
```js
async function handleIceCandidate(candidate) {
    try {
        await pc2.addIceCandidate(candidate);
    } catch (error) {
        console.error('Ошибка добавления ICE кандидата:', error);
    }
}
```


### Полная последовательность
1. ✅ Инициализация - оба пира создают RTCPeerConnection
2. ✅ Настройка обработчиков - настраивают onicecandidate
3. ✅ Peer1 создает offer → отправляет Peer2
4. ✅ Peer2 получает offer → устанавливает как remote description
5. ✅ Peer2 создает answer → отправляет Peer1
6. ✅ Peer1 получает answer → устанавливает как remote description
7. 🔄 Обмен ICE кандидатами - начинается параллельно с шага 3
8. ✅ Соединение установлено - когда собраны все кандидаты

### Важные моменты:
1. ICE кандидаты начинают собираться сразу после создания предложения/ответа
2. Обмен кандидатами происходит параллельно с обменом SDP
3. Кандидаты можно добавлять в любое время, даже до установки remote description
4. Событие oniceconnectionstatechange покажет статус соединения

### Состояния соединения:
```js
pc1.onconnectionstatechange = () => {
    console.log('Состояние соединения:', pc1.connectionState);
    // new, connecting, connected, disconnected, failed, closed
};

pc1.oniceconnectionstatechange = () => {
    console.log('ICE состояние:', pc1.iceConnectionState);
    // new, checking, connected, completed, failed, disconnected, closed
};
```
