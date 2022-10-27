<template>
  <div class="container">
    <div v-if="currentContent.type === 'video/mp4'" class="video" ref="video">
      <video
        id="my-player"
        class="video-js vjs-16-9"
        controls
        preload="auto"
        width="100%"
        height="100%"
      ></video>
    </div>
    <p v-if="currentContent.type === 'text'">{{ currentContent.src }}</p>
    <nav>
      <ul>
        <li @click="getNextVideo(1, 'video/mp4')">Video 01</li>
        <li @click="getNextVideo(2, 'video/mp4')">Video 02</li>
        <li @click="getNextVideo(3, 'text')">Texto 01</li>
        <li @click="getNextVideo(4, 'video/mp4')">Video 03</li>
      </ul>
    </nav>
  </div>
</template>

<style>
.container {
  display: flex;
  width: 100%;
  height: 100%;
}

.video {
  width: 100%;
  height: 100%;
}

.video-js {
  width: 100%;
  height: 100%;
}

nav {
  display: flex;
  width: 300px;
}

p {
  width: 100%;
  display: flex;
  color: white;
  font-size: 10rem;
}

li {
  background-color: aquamarine;
  margin-bottom: 20px;
  text-decoration: none;
  list-style: none;
  padding: 1rem;
  border-radius: 0.5rem;
  text-transform: uppercase;
}
</style>

<script>
import videojs from '@mux/videojs-kit';
import '@mux/videojs-kit/dist/index.css';

export default {
  mounted() {
    this.player = videojs('my-player', {
      timelineHoverPreviews: true,
      plugins: {
        mux: {
          debug: false,
          data: {
            env_key: 'gjXXXXXX',
            video_title: 'Example Title',
          },
        },
      },
    });

    this.player.src({
      src: 'https://edisciplinas.usp.br/pluginfile.php/5196097/mod_resource/content/1/Teste.mp4',
      type: 'video/mp4',
    });
  },

  data() {
    return {
      videos: [
        {
          id: 1,
          src: 'https://edisciplinas.usp.br/pluginfile.php/5196097/mod_resource/content/1/Teste.mp4',
          type: 'video/mp4',
        },
        {
          id: 2,
          src: 'https://edisciplinas.usp.br/pluginfile.php/5196097/mod_resource/content/1/Teste.mp4',
          type: 'video/mp4',
        },
        {
          id: 3,
          src: 'Isso é um TEXTO!!!!',
          type: 'text',
        },
        {
          id: 4,
          src: 'https://edisciplinas.usp.br/pluginfile.php/5196097/mod_resource/content/1/Teste.mp4',
          type: 'video/mp4',
        },
      ],
      currentContent: {
        id: 1,
        src: 'https://edisciplinas.usp.br/pluginfile.php/5196097/mod_resource/content/1/Teste.mp4',
        type: 'video/mp4',
      },
      player: null,
    };
  },

  methods: {
    getNextVideo(id, type) {
      this.currentContent = this.videos.find(
        (video) => video.id === id && video.type === type
      );

      if (this.currentContent.type === 'video/mp4') {
        this.player.src({
          src: this.currentContent.src,
          type: this.currentContent.type,
        });
      }
    },
  },
};
</script>
