<template>
  <div class="valentine-Container">
    <div class="bg_heart" ref="bgHeart"></div>

    <div id="cat-jumping" style="max-width: 20%">
      <img
        src="https://media.tenor.com/1ULtxe1Wv10AAAAi/smile-peach-cat.gif"
        alt="cat-jumping"
      />
    </div>
    <div id="cat-kissing" style="max-width: 20%">
      <img
        src="https://media.tenor.com/TBwDXMpmFXUAAAAi/peach-and-goma-peach-goma.gif"
        alt="cat-kissing"
      />
    </div>

    <div style="">
      <div
        id="text"
        style="font-size: 26px; font-weight: 500; padding-left: 80px"
      >
        {{ Title }}
      </div>

      <div
        id="yesPressed"
        style="
          display: none;
          justify-content: center;
          font-size: 26px;
          font-weight: 500;
        "
      >
        <p>{{ Answer }}</p>
      </div>

      <div id="button" style="padding-left: 80px; margin-left: 60px">
        <button
          :style="{ fontSize: firstButtonFontSize + 'em' }"
          @click="handleYesPressed"
          id="yesButton"
        >
          Yes
        </button>
        <button style="margin-left: 15px" id="noButton" @click="noPressed">
          {{ phrases[phase] }}
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      phrases: [
        "No",
        "Are u sure?",
        "Really sure?",
        "Don't do this to me",
        "I'm gonna cry",
        "You're breaking my heart",
      ],
      Title: "Will you be my valentine?",
      Answer: "Yayy!!!",
      loveInterval: null,
      phase: 0,
      firstButtonFontSize: 1,
    };
  },
  created() {
    // This hook is fired after the instance has been created but before the template is mounted.
    // You can perform additional setup here if needed.
  },
  methods: {
    noPressed() {
      this.phase = (this.phase + 1) % this.phrases.length;
      this.firstButtonFontSize += 4;
      console.log(this.firstButtonFontSize);
    },
    handleYesPressed() {
      document.getElementById("yesPressed").style.display = "inline-block";
      document.getElementById("text").style.display = "none";
      document.getElementById("button").style.display = "none";
      document.getElementById("cat-jumping").style.display = "none";
      document.getElementById("cat-kissing").style.display = "block";
      this.loadLoveAnimation();
    },
    loadLoveAnimation() {
      this.loveInterval = setInterval(() => {
        const r_num = Math.floor(Math.random() * 40) + 1;
        const r_size = Math.floor(Math.random() * 65) + 10;
        const r_left = Math.floor(Math.random() * 100) + 1;
        const r_bg = Math.floor(Math.random() * 25) + 100;
        const r_time = Math.floor(Math.random() * 5) + 5;

        const bgHeart = this.$refs.bgHeart;

        // Create heart elements
        const heart = document.createElement("div");
        heart.className = "heart";
        heart.style.width = r_size + "px";
        heart.style.height = r_size + "px";
        heart.style.left = r_left + "%";
        heart.style.background = `rgba(255, ${r_bg - 25}, ${r_bg}, 1)`;
        heart.style.animation = `love ${r_time}s ease`;

        const heart2 = document.createElement("div");
        heart2.className = "heart";
        heart2.style.width = r_size - 10 + "px";
        heart2.style.height = r_size - 10 + "px";
        heart2.style.left = r_left + r_num + "%";
        heart2.style.background = `rgba(255, ${r_bg - 25}, ${r_bg + 25}, 1)`;
        heart2.style.animation = `love ${r_time + 5}s ease`;

        // Append hearts to the bg_heart element
        bgHeart.appendChild(heart);
        bgHeart.appendChild(heart2);

        // Remove hearts if necessary
        bgHeart.querySelectorAll(".heart").forEach((heart) => {
          let top = heart.style.top.replace(/[^-\d\.]/g, "");
          let width = heart.style.width.replace(/[^-\d\.]/g, "");
          if (top <= -100 || width >= 150) {
            heart.remove();
          }
        });
      }, 500);
    },
  },
  beforeUnmount() {
    // Clear the interval when the component is about to be destroyed
    clearInterval(this.loveInterval);
  },
  mounted() {
    document.getElementById("cat-kissing").style.display = "none";
  },
};
</script>

<style scoped>
.valentine-Container {
  position: absolute;
  z-index: 10;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100%;
  width: 100%;
}

#noButton {
  background-color: #ff4d4d;
  color: white;
  border: none;
  padding: 10px 20px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
  border-radius: 12px;
}

#yesButton {
  background-color: #2dff9d;
  color: white;
  border: none;
  padding: 10px 20px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
  border-radius: 12px;
}

html,
body {
  height: 100%;
  margin: 0; /* Remove default margin */
}

.bg_heart {
  position: absolute;
  z-index: -1;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
}

.heart {
  position: absolute;
  top: -50%;
  -webkit-transform: rotate(-45deg);
  -moz-transform: rotate(-45deg);
  -m-transform: rotate(-45deg);
  transform: rotate(-45deg);
}

.heart:before,
.heart:after {
  position: absolute;
  top: -50%;
  left: 0;
  display: block;
  content: "";
  width: 100%;
  height: 100%;
  background: inherit;
  border-radius: 100%;
}

.heart:after {
  position: absolute;
  top: 0;
  right: -50%;
}

@-webkit-keyframes love {
  0% {
    top: 110%;
  }
}

@-moz-keyframes love {
  0% {
    top: 110%;
  }
}

@-ms-keyframes love {
  0% {
    top: 110%;
  }
}

@keyframes love {
  0% {
    top: 110%;
  }
}

/* Media Query for Small Screens */
@media only screen and (max-width: 600px) {
  .valentine-Container {
    padding: 20px; /* Adjust padding for smaller screens */
  }
 
  #text {
    font-size: 18px; /* Adjust font size for smaller screens */
    padding-left: 20px;
  }

  #button {
    padding-left: 20px;
    margin-left: 20px;
  }
}
</style>
