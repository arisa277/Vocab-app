<template>
  <div class="questionspage">
    <nuxt-child />
  </div>
</template>

<style>
.title h1 {
  color: #49634b;
  margin-bottom: 50px;
}
.questionspage {
  height: 100vh;
  text-align: center;
  background: #ded2c2;
  display: flex;
  justify-content: center;
  align-items: center;
}
.question {
  color: #cb847a;
  font-size: 30px;
  font-weight: bold;
}
.input {
  margin: 10px 0;
  outline: none;
  border: none;
  width: 80%;
  height: 30px;
  font-size: 100%;
  text-align: center;
}
.start-btn {
  background: #49634b;
  border: none;
  width: 200px;
  padding: 7px;
  cursor: pointer;
  font-weight: bold;
  font-size: 18px;
  color: #fff;
}
.start-btn:hover {
  background: rgb(53, 79, 55);
}

.submit-btn {
  background: #49634b;
  border: none;
  width: 80%;
  padding: 7px;
  cursor: pointer;
  font-weight: bold;
  font-size: 18px;
  color: #fff;
}
.restart-btn {
  background: #49634b;
  border: none;
  width: 100%;
  padding: 7px;
  cursor: pointer;
  font-weight: bold;
  font-size: 18px;
  color: #fff;
}
.restart-btn:hover {
  background: rgb(53, 79, 55);
}
.qtext {
  font-size: 18px;
  color: #202020;
}
.back_btn {
  margin-top: 50px;
}
.back_btn a {
  text-decoration: none;
  color: #cb847a;
}
</style>
