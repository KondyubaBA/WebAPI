# RTCPeerConnection

## Свойства

1. **canTrickleIceCandidates**
   - **Тип**: `boolean`
   - **Описание**: Указывает, поддерживает ли соединение "трикинг" ICE-кандидатов. Если `true`, ICE-кандидаты могут быть отправлены по мере их получения.

2. **connectionState**
   - **Тип**: `string`
   - **Описание**: Текущее состояние соединения. Возможные значения: 
     - `"new"`: соединение создано, но не было установлено.
     - `"connecting"`: соединение в процессе установления.
     - `"connected"`: соединение успешно установлено.
     - `"disconnected"`: соединение временно потеряно.
     - `"failed"`: соединение не удалось установить.
     - `"closed"`: соединение закрыто.

3. **currentLocalDescription**
   - **Тип**: `RTCSessionDescription`
   - **Описание**: Текущее локальное описание (SDP) соединения. Это описание, которое в данный момент используется в соединении.

4. **currentRemoteDescription**
   - **Тип**: `RTCSessionDescription`
   - **Описание**: Текущее удаленное описание (SDP) соединения. Это описание, которое в данный момент используется для удаленного пира.

5. **iceConnectionState**
   - **Тип**: `string`
   - **Описание**: Текущее состояние ICE-соединения. Возможные значения:
     - `"new"`
     - `"checking"`
     - `"connected"`
     - `"completed"`
     - `"disconnected"`
     - `"failed"`
     - `"closed"`

6. **iceGatheringState**
   - **Тип**: `string`
   - **Описание**: Текущее состояние сбора ICE-кандидатов. Возможные значения:
     - `"new"`
     - `"gathering"`
     - `"complete"`

7. **localDescription**
   - **Тип**: `RTCSessionDescription` или `null`
   - **Описание**: Локальное описание (SDP), которое было установлено с помощью `setLocalDescription()`.

8. **onaddstream**
   - **Тип**: `EventHandler`
   - **Описание**: Обработчик события, вызываемый, когда новый медиапоток добавляется к соединению.

9. **onconnectionstatechange**
   - **Тип**: `EventHandler`
   - **Описание**: Обработчик события, вызываемый при изменении состояния соединения.

10. **ondatachannel**
    - **Тип**: `EventHandler`
    - **Описание**: Обработчик события, вызываемый, когда удаленный пир создает новый `DataChannel`.

11. **onicecandidate**
    - **Тип**: `EventHandler`
    - **Описание**: Обработчик события, вызываемый, когда новый ICE-кандидат становится доступным.

12. **onicecandidateerror**
    - **Тип**: `EventHandler`
    - **Описание**: Обработчик события, вызываемый при возникновении ошибки во время создания ICE-кандидатов.

13. **oniceconnectionstatechange**
    - **Тип**: `EventHandler`
    - **Описание**: Обработчик события, вызываемый при изменении состояния ICE-соединения.

14. **onicegatheringstatechange**
    - **Тип**: `EventHandler`
    - **Описание**: Обработчик события, вызываемый при изменении состояния сбора ICE-кандидатов.

15. **onnegotiationneeded**
    - **Тип**: `EventHandler`
    - **Описание**: Обработчик события, вызываемый, когда требуется новое соглашение о параметрах соединения.

16. **onremovestream**
    - **Тип**: `EventHandler`
    - **Описание**: Обработчик события, вызываемый, когда медиапоток удаляется из соединения.

17. **ontrack**
    - **Тип**: `EventHandler`
    - **Описание**: Обработчик события, вызываемый, когда добавляется новый медиапоток или трек.

18. **pendingLocalDescription**
    - **Тип**: `RTCSessionDescription` или `null`
    - **Описание**: Локальное описание, ожидающее применения с помощью `setLocalDescription()`.

19. **pendingRemoteDescription**
    - **Тип**: `RTCSessionDescription` или `null`
    - **Описание**: Удаленное описание, ожидающее применения с помощью `setRemoteDescription()`.

20. **remoteDescription**
    - **Тип**: `RTCSessionDescription` или `null`
    - **Описание**: Удаленное описание (SDP), которое было установлено с помощью `setRemoteDescription()`.

21. **sctp**
    - **Тип**: `RTCSctpTransport` или `null`
    - **Описание**: Объект, представляющий SCTP (Stream Control Transmission Protocol) для передачи данных.

22. **signalingState**
    - **Тип**: `string`
    - **Описание**: Текущее состояние сигнализации. Возможные значения:
      - `"stable"`
      - `"have-local-offer"`
      - `"have-remote-offer"`
      - `"have-local-pranswer"`
      - `"have-remote-pranswer"`
      - `"closed"`
