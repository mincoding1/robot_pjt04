<template>
  <div class="remote-container">
    <div class="project-list">
      <div class="project" id="pjt02">pjt02</div>
      <div class="project" id="pjt03">pjt03</div>
      <div class="project" id="pjt04">pjt04</div>
    </div>
    <div class="dashboard">
      <div class="title">
        <b>Remote Controller</b>
      </div>
      <div class="chat-container">
        <div class="chat-log">
          <div v-for="(msg, index) in chatLog" :key="index" :class="msg.role">
            <span>{{ msg.content }}</span>
          </div>
        </div>
        <div class="chat-input">
          <textarea v-model="userInput" placeholder="질문을 입력하세요" @keyup="handleKeyUp" ></textarea>
          <button @click="sendQuestion">질문 보내기</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

// 사용자 입력과 GPT 응답 상태
const userInput = ref("");
const chatLog = ref([]);

function handleKeyUp(event) {
  if (event.key === "Enter") {
    if (event.altKey) {
      // Alt + Enter: 줄 바꾸기
      userInput.value += "\n";
    } else {
      // Enter: sendQuestion 호출
      event.preventDefault();
      sendQuestion();
    }
  }
}

const sendQuestion = async () => {
  if (userInput.value.trim() === "") return;

    // 대화 기록에 사용자 입력 추가
    chatLog.value.push({ role: "user", content: userInput.value });

    // 요구 사항 1. OpenAI API 를 활용한 챗봇 기능 구현

    // 요구 사항 2. 챗봇의 응답을 통해 라즈베리파이 컨트롤

    userInput.value = "";
};
</script>

<style scoped>
.remote-container {
  display: flex;
  min-width: 90rem;
  min-height: 50vh;
  max-height: 80vh;
  margin: 0 auto;
  padding: 20px;
  background-color: #eceeeb;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
  border-radius: 10px;
  gap: 20px;
}

.project-list {
  display: flex;
  flex-direction: column;
  margin-right: 10px;
  padding: 1rem;
  border-right: 1px solid #c1d0d7;
}

.project {
  width: 100px;
  height: 50px;
  border: 2px solid black;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 10px;
  cursor: pointer;
  background-color: #fff;
  border-radius: 5px;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.1);
}

.project:hover {
    background-color: #98fb98;
}

#pjt04 {
    background-color: #87ceeb;
}

#pjt04:hover {
    background-color: #98fb98;
}

.dashboard {
  flex: 1;
}

.title {
  position: relative;
  display: inline;
  top: 10px;
  left: 10px;
  background-color: #eceeeb;
  padding: 0 10px;
  font-size: 1.2rem;
  z-index: 1;
}

.chat-container {
  flex: 1;
  display: flex;
  padding: 1rem;
  border: 1px solid #C1D0D7;
  flex-direction: column;
  height: 90%;
  border: 1px solid #c1d0d7;
  border-radius: 10px;
}

.chat-log {
  flex: 1;
  padding: 1rem;
  padding-left: 2rem;
  padding-right: 2rem;
  overflow-y: auto;
  background-color: #f5f5f5;
  font-size: 1.2rem;
}

.chat-log .user {
  text-align: right;
}

.chat-log .assistant {
  text-align: left;
}

.chat-log span {
  display: inline-block;
  margin: 5px 0;
  padding: 10px;
  border-radius: 10px;
  max-width: 80%;
  word-wrap: break-word;
}

.chat-log .user span {
  background-color: #d1ecf1;
  color: #0c5460;
}

.chat-log .assistant span {
  background-color: #d4edda;
  color: #155724;
}

.chat-input {
  display: flex;
  border-top: 1px solid #c1d0d7;
  padding: 10px;
  background-color: #fff;
}

.chat-input textarea {
  flex: 1;
  height: 50px;
  padding: 10px;
  border: 1px solid #c1d0d7;
  border-radius: 5px;
  resize: none;
}

.chat-input button {
  margin-left: 10px;
  padding: 1rem;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 1rem;
  font-weight: 600;
}

.chat-input button:hover {
  background-color: #0056b3;
}
</style>
