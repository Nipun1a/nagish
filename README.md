# nagish
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nagish App</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <header>
        <h1>Nagish App</h1>
    </header>
    <main>
        <div class="container">
            <div id="chat-window" class="chat-window">
                <!-- Messages will appear here -->
            </div>
            <div class="input-area">
                <textarea id="message-input" placeholder="Type your message here..."></textarea>
                <button id="send-btn">Send</button>
                <button id="record-btn">🎤</button>
            </div>
        </div>
    </main>
    <script src="script.js"></script>
</body>
</html>
// js code
document.addEventListener('DOMContentLoaded', () => {
    const sendButton = document.getElementById('send-btn');
    const recordButton = document.getElementById('record-btn');
    const messageInput = document.getElementById('message-input');
    const chatWindow = document.getElementById('chat-window');
    // Speech synthesis (text-to-speech)
    function speakMessage(text) {
        const utterance = new SpeechSynthesisUtterance(text);
        window.speechSynthesis.speak(utterance);
    }
    sendButton.addEventListener('click', () => {
        const message = messageInput.value;
        if (message) {
            // Display the message in chat window
            chatWindow.innerHTML += `<div class="message sent">${message}</div>`;
            messageInput.value = '';
             // Convert text to speech
            speakMessage(message);
        }
    });
   // Speech recognition (speech-to-text)
    const recognition = new (window.SpeechRecognition || window.webkitSpeechRecognition)();
    recognition.lang = 'en-IN'; // Set language to Indian English
        recognition.onresult = event => {
        const transcript = event.results[0][0].transcript;
        chatWindow.innerHTML += `<div class="message received">${transcript}</div>`;
        speakMessage(transcript); // Optional: Convert received message to speech
    };
    recordButton.addEventListener('click', () => {
        recognition.start();
    });
});
//css page
body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
    background-color: #f0f0f0;
}

header {
    background-color: #007bff;
    color: white;
    padding: 10px 0;
    text-align: center;
}

.container {
    width: 80%;
    margin: 20px auto;
}

.chat-window {
    background: white;
    border: 1px solid #ddd;
    height: 400px;
    overflow-y: scroll;
    padding: 10px;
    margin-bottom: 10px;
}

.input-area {
    display: flex;
    flex-direction: column;
}

textarea {
    width: 100%;
    height: 100px;
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
    margin-bottom: 10px;
    resize: none;
}

button {
    background-color: #007bff;
    color: white;
    border: none;
    padding: 10px;
    border-radius: 5px;
    cursor: pointer;
    margin-top: 5px;
}

button:hover {
    background-color: #0056b3;
}

