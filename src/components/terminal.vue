<template>
  <div class="terminal--container">
    <div class="terminal--starter">
      <p class="line1">
        {{ msg1 }} <span class="name--tag">{{ name }}</span>
      </p>
      <p>
        <span>{{ msg2 }}</span>
      </p>
      <div>
        <p>
          This is a web terminal to introduce my self and my work please use
        </p>
        <p><span style="color: yellow">/help </span>to see the commands</p>
      </div>
      <p>
        Also you can follow my work and contact me from :
        <span class="type"></span>
      </p>
      <a href="#"><h4>pooyaworkjs@gmail.com</h4></a>
      <a href="https://github.com/Redskullvue">Github</a>
      <a href="https://www.instagram.com/po0ya_g/"><h4>Instagram</h4></a>
    </div>
    <div v-for="enter in enterCount" :key="enter" class="input--container">
      <form @submit.prevent="commandLine()">
        <label>~/Pooya >></label>
        <input
          class="input"
          type="text"
          placeholder="Try /help"
          v-model="inputValue"
        />
      </form>
    </div>
    <div v-if="help" class="help--section">
      <ul class="help--list">
        <li>Here Are the list of commands :</li>
        <li v-for="command in commandsInfo" :key="commandsInfo[command]">
          {{ command }}
        </li>
      </ul>
    </div>
    <div v-if="showProject" class="projects--list">
      <ul class="help--list">
        <li v-for="project in projects" :key="project.link">
          <a :href="project.link">{{ project.name }} </a>
        </li>
      </ul>
    </div>
    <div v-if="wrongCommand">
      <p>
        <span style="color: yellow">{{ lastInputValue }}</span> is not a command
        please try /help to see the commands
      </p>
    </div>
    <div v-if="about" class="about">
      <p>
        I'm a <span style="color: yellow">front-end developer</span> who loves
        web and every single detail about it
      </p>
      <p>
        I can build websites from scratch also have a good undrestanding of
        <span style="color: yellow">JavaScript</span> and
        <span style="color: yellow">Vue Js</span>
      </p>
    </div>
    <div v-if="skills" class="skills-list">
      <p><span>Programming Language :</span> JavaScript</p>
      <p>
        <span>FrameWorks and Libraries : </span> Vue js , Nuxt js , TailwindCSS
        , Axios , WebPack , Vue Router , VueX , Vue Cli
      </p>
      <p><span>Dev Tools : </span> Visual Studio Code , Git , NPM ~ Yarn</p>
      <p><span>OS : </span> Ubuntu 20 + , Windows</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "terMinal",
  props: {
    msg1: String,
    msg2: String,
    name: String,
  },

  data() {
    return {
      //Getting value of the main input
      inputValue: "",
      //This Variable is to show to user what command he/she used wrong
      lastInputValue: "",
      // These are to toggle what get renders on the terminal main page
      help: false,
      skills: false,
      about: false,
      showProject: false,
      wrongCommand: false,
      projects: [
        { name: "splustuning", link: "https://splustuning.netlify.app/" },
        { name: "UPA", link: "https://upatest.netlify.app/" },
        {
          name: "Delicious Food",
          link: "https://deliciousfoodlayout.netlify.app/",
        },
        { name: "ToDo App", link: "https://todovue1.netlify.app/" },
        { name: "Calculator", link: "https://mycalculatorvue.netlify.app/" },
        { name: "WeatherApp", link: "https://myvueweatherapp1.netlify.app/" },
      ],
      commandsInfo: ["/help", "/skills", "/about", "/clear", "/projects"],
      //These two are used to add another input to terminal
      enterCount: ["0"],
      mainCounter: 0,
    };
  },

  methods: {
    //This whole thing is to handle what gets rendered in the terminal of course none of it is neccessary
    commandLine() {
      if (this.inputValue === "/help") {
        this.help = true;
        this.wrongCommand = false;
        this.skills = false;
        this.showProject = false;
        this.about = false;
      } else if (this.inputValue === "/clear") {
        this.help = false;
        this.skills = false;
        this.about = false;
        this.showProject = false;
        this.wrongCommand = false;
        this.enterCount.splice(0, this.enterCount.length);
      } else if (this.inputValue === "/projects") {
        this.showProject = true;
        this.skills = false;
        this.help = false;
        this.about = false;
        this.wrongCommand = false;
      } else if (this.inputValue === "/about") {
        this.about = true;
        this.showProject = false;
        this.help = false;
        this.skills = false;
        this.wrongCommand = false;
      } else if (this.inputValue === "/skills") {
        this.about = false;
        this.help = false;
        this.showProject = false;
        this.wrongCommand = false;
        this.skills = true;
      } else {
        this.lastInputValue = this.inputValue;
        this.help = false;
        this.skills = false;
        this.about = false;
        this.showProject = false;
        this.wrongCommand = true;
      }
      //We wanted to generate new inputs in the terminal
      let terminalInputs = document.querySelectorAll("input");
      this.inputValue = "";
      terminalInputs[this.mainCounter].setAttribute("disabled", "");
      terminalInputs[this.mainCounter].setAttribute("placeholder", "");
      terminalInputs[this.mainCounter].style = "display : none";
      this.enterCount.push(this.mainCounter++);
    },
  },
};
</script>

<style>
* {
  font-family: monospace;
  font-size: 18px;
}
body {
  background-color: #13012d;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}
.terminal--container {
  background-color: #13012d;
  width: 700px;
  height: max-content;
  padding: 30px;
  margin: 30px;
  color: #fff;
}
.terminal--starter {
  animation: fadeIn 1.5s steps(52);
  overflow: hidden;
  white-space: nowrap;
}

.type {
  height: 1px;
  width: 1px;
  background-color: black;
  border-right: solid 1px #fff;
  margin-left: 4px;
  animation: dot 1s infinite;
}
.name--tag {
  color: yellow;
}
.input--container {
  margin-top: 20px;
}
.input {
  background-color: inherit;
  border: none;
  outline: none;
  color: yellow;
}
.help--list li {
  list-style: none;
  margin: 10px;
}
.skills-list span {
  color: yellow;
}
a {
  color: yellow;
  text-decoration: none;
}
@keyframes fadeIn {
  from {
    width: 0;
  }
  to {
    width: 100%;
  }
}
@keyframes dot {
  from {
    opacity: 0;
  }
  50% {
    opacity: 1;
  }
  to {
    opacity: 0;
  }
}
</style>
