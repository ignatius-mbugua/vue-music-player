<template>
  <div class="row pt-5">
    <div class="col-sm-12 col-md-6 mx-auto">
      <!-- Card -->
      <div class="card">
        <div class="card-body text-center">
          <!-- Image -->
          <img
            id="music_art"
            :src="require(`@/assets/images/${songs[song_index]}.jpg`)"
            alt="music-art"
            class="img-fluid"
            width="300"
            height="200"
          />
          <!-- Audio -->
          <audio id="music" ref="ref_music">
            <source
              :src="require(`@/assets/music/${songs[song_index]}.mp3`)"
              type="audio/ogg"
            />
            Your broswer doesn't support the audio element
          </audio>
          <!-- Music Info -->
          <h5 class="pt-3">{{ songs[song_index] }}</h5>
          <!-- Progress Bar -->
          <div class="progress">
            <div
              class="progress-bar"
              role="progressbar"
              aria-valuenow="0"
              aria-valuemin="0"
              aria-valuemax="100"
            ></div>
          </div>
          <!-- Control buttons -->
          <div class="pt-4">
            <button
              type="button"
              class="btn btn-outline-primary float-left"
              @click="previousSong"
            >
              <font-awesome-icon icon="step-backward" size="2x" />
            </button>
            <button
              type="button"
              class="btn btn-outline-primary"
              @click="playOrPauseSong"
            >
              <font-awesome-icon icon="play" v-if="!is_playing" size="2x" />
              <font-awesome-icon icon="pause" v-else size="2x" />
            </button>
            <button
              type="button"
              class="btn btn-outline-primary float-right"
              @click="nextSong"
            >
              <font-awesome-icon icon="step-forward" size="2x" />
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "MusicCard",
  data() {
    return {
      is_playing: false,
      song_index: 0,
      songs: ["hey", "summer", "ukulele"],
    };
  },
  methods: {
    // play and pause song
    playOrPauseSong() {
      if (!this.is_playing) {
        this.$refs.ref_music.play();
      } else {
        this.$refs.ref_music.pause();
      }
      this.is_playing = !this.is_playing;
    },

    // previous song
    previousSong() {
      let previous_song_index = this.song_index - 1;
      if (previous_song_index < 0) {
        this.song_index = this.songs.length - 1;
      } else {
        this.song_index = previous_song_index;
      }
      // load song
      this.$refs.ref_music.load();
      if (this.is_playing) {
        this.$refs.ref_music.play();
      }
    },

    // next song
    nextSong() {
      let next_song_index = this.song_index + 1;
      if (next_song_index > this.songs.length - 1) {
        this.song_index = 0;
      } else {
        this.song_index = next_song_index;
      }
      // load song
      this.$refs.ref_music.load();
      if (this.is_playing) {
        this.$refs.ref_music.play();
      }
    },
  },
};
</script>
