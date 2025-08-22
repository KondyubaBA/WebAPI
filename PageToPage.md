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
