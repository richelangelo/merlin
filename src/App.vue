<template>
  <div id="app">
  <!--<p>Playing {{ playing }}</p>
    <p>CurrentScene {{ currentScene }}</p>
    <p>scenesCount {{ scenesCount }}</p> -->

    <!-- controls -->
    <nav class="controls" v-if="currentScene > 0">
      <img
        id="buttons"
        src="/pictures/a/back.png"
        alt="back"
        @click="
          minusScene();
          playFile();
        "
      />
      <div class="play-pause">
        <img
          id="buttons"
          src="/pictures/a/play.png"
          alt="play"
          v-if="!playing"
          @click="
            togglePlaying();
            playFile();
          "
        />
        <img
          id="buttons"
          src="/pictures/a/pause.png"
          alt="pause"
          v-if="playing === true"
          @click="
            togglePlaying();
            pauseFile();
          "
        />
      </div>
      <img
        id="buttons"
        src="/pictures/a/next.png"
        alt="next"
        @click="plusScene"
        v-if="currentScene < (scenesCount - 1)"
      />
    </nav>

    <!-- Start Screen -->
    <div class="startscreen" v-if="currentScene === 0">
      <img
        id="start"
        src="/pictures/a/start.png"
        alt="next"
        @click="currentScene++"
      />
    </div>

    <!-- scenes -->
    <ul class="scenes">
      <div
        v-for="(scene, index) in scenesCount"
        :key="index"
        v-show="index === currentScene"
      >
        <img
          id="picture"
          :src="`/pictures/a/picture_${index}.png`"
          alt="reload"
        />
        <!-- <p>{{ scene - 1 }}</p >-->
        <!-- <audio id="audio-player">
          <source src="/sounds/b/mp3/mer_1.mp3" type="audio/mpeg" />
          Your browser does not support the audio tag.
        </audio>
        <audio id="mer_1" preload="auto" controls>
          <source
            :src="`/sounds/b/mp3/mer_${scene - 1}.mp3`"
            preload="auto"
            type="audio/mpeg"
          /> 
          hey
        </audio>-->
      </div>
    </ul>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      playing: false,
      currentScene: 0,
      scenesCount: 27,
      audio: new Audio(), //
    };
  },

  methods: {
    togglePlaying() {
      console.log("play");
      this.playing = !this.playing;
    },

    minusScene() {
      console.log("minus");
      this.currentScene > 0 ? this.currentScene-- : (this.currentScene = 0);
    },
    plusScene() {
      console.log("plus");
      this.currentScene < (this.scenesCount - 1)
        ? this.currentScene++
        : (this.currentScene = this.scenesCount - 1);

      this.playFile();
    },

    playFile() {
      //
      if (this.currentScene < 1) {
        this.pauseFile();
        return;
      }
      this.audio.src = "/sounds/b/mp3/mer_" + this.currentScene + ".mp3";
      console.log("audio", this.audio);
      this.audio.play();
      this.playing = true;
    },

    pauseFile() {
      //
      console.log("pause?", this.audio);
      this.audio.pause();
      this.playing = false;
    },

    //Toggle Audio
    /* toggleAudio() {
      console.log("toggle?");

      var audio = document.getElementById("audio-player");
      if (audio.paused) {
        audio.play();
      } else {
        audio.pause();
      }
    },*/
  },
};
</script>

<style>
body {
  background-color: black;
  color: white;
  margin: 0;
  padding: 0;
  overflow: hidden;
}

#app {
  height: 100%;
  min-height: 100vh;
}

#picture {
  width: 100%;
  display: flex;
  justify-content: center;
}

#buttons {
  width: 200px;
}

#start {
  width: 300px;
}

.startscreen {
  display: flex;
  justify-content: center;
}

.controls {
  display: flex;
  justify-content: center;
}
</style>
