<template>
  <div class="row pt-5">
    <div class="col-sm-12 col-md-6 mx-auto">
      <!-- Card -->
      <div class="card">
        <div class="card-body text-center">
          <!-- Image -->
          <img
            id="music_art"
            :src="require(`@/assets/images/${songs[song_index].name}.jpg`)"
            alt="music-art"
            class="img-fluid rounded-lg shadow-lg"
            width="300"
            height="200"
          />
          <!-- Audio -->
          <audio
            id="music"
            ref="ref_music"
            @ended="nextSong"
            @timeupdate="timeUpdate"
          >
            <source
              :src="require(`@/assets/music/${songs[song_index].name}.mp3`)"
              type="audio/ogg"
            />
            Your broswer doesn't support the audio element
          </audio>
          <!-- Music Info -->
          <div class="py-3">
            <h4>{{ songs[song_index].title }}</h4>
            <p class="text-muted">{{ songs[song_index].artist }}</p>
          </div>
          <!-- Audio Time -->
          <div class="d-flex justify-content-between">
            <span id="currentTime">{{ song_current_time }}</span>
            <span id="songDuration">{{ song_duration }}</span>
          </div>
          <!-- Progress Bar -->
          <div
            class="progress"
            ref="ref_main_progress"
            @click="changeCurrentTime($event)"
          >
            <div
              class="progress-bar"
              role="progressbar"
              :style="{ width: progress_width + '%' }"
              :aria-valuenow="progress_width"
              aria-valuemin="0"
              aria-valuemax="100"
            ></div>
          </div>
          <!-- Control buttons -->
          <div class="pt-4">
            <font-awesome-icon
              icon="step-backward"
              size="2x"
              @click="previousSong"
            />
            <font-awesome-icon
              icon="play"
              v-if="!is_playing"
              size="2x"
              class="ml-5"
              @click="playOrPauseSong"
            />
            <font-awesome-icon
              icon="pause"
              v-else
              size="2x"
              class="ml-5"
              @click="playOrPauseSong"
            />
            <font-awesome-icon
              icon="step-forward"
              size="2x"
              class="ml-5"
              @click="nextSong"
            />
          </div>
          <!-- Track Numbers -->
          <div class="pt-4">
            <p class="text-muted">{{ song_index + 1 }} / {{ songs.length }}</p>
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
      songs: [
        {
          title: "Hey",
          artist: "Benjamin Tissot",
          name: "hey",
        },
        {
          title: "Summer",
          artist: "Benjamin Tissot",
          name: "summer",
        },
        {
          title: "Ukulele",
          artist: "Benjamin Tissot",
          name: "ukulele",
        },
        {
          title: "Buddy",
          artist: "Benjamin Tissot",
          name: "buddy",
        },
        {
          title: "Energy",
          artist: "Benjamin Tissot",
          name: "energy",
        },
        {
          title: "Evolution",
          artist: "Benjamin Tissot",
          name: "evolution",
        },
        {
          title: "Funny Song",
          artist: "Benjamin Tissot",
          name: "funnysong",
        },
        {
          title: "Happy Rock",
          artist: "Benjamin Tissot",
          name: "happyrock",
        },
        {
          title: "Moose",
          artist: "Benjamin Tissot",
          name: "moose",
        },
        {
          title: "Sunny",
          artist: "Benjamin Tissot",
          name: "sunny",
        },
      ],
      song_duration: "0:00",
      song_current_time: "0:00",
      progress_width: "0",
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
      this.progress_width = 0;
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
      this.progress_width = 0;
      if (this.is_playing) {
        this.$refs.ref_music.play();
      }
    },

    // format time
    formatTime(currentTime) {
      if (isNaN(currentTime)) {
        return "0:00";
      }
      let minutes = Math.floor(currentTime / 60);
      let seconds = Math.floor(currentTime % 60);
      seconds = seconds >= 10 ? seconds : "0" + (seconds % 60);
      let formatTime = minutes + ":" + seconds;
      return formatTime;
    },

    // time update
    timeUpdate() {
      let duration = this.$refs.ref_music.duration;
      let currentTime = this.$refs.ref_music.currentTime;
      // progressbar
      this.progress_width = ((currentTime / duration) * 100).toFixed(2);
      // song timings
      this.song_current_time = this.formatTime(parseInt(currentTime));
      this.song_duration = this.formatTime(duration);
    },

    // set progressbar on click
    changeCurrentTime(event) {
      let duration = this.$refs.ref_music.duration;
      let main_progress_width = this.$refs.ref_main_progress.clientWidth;
      let click_offset = event.offsetX;
      this.$refs.ref_music.currentTime =
        (click_offset / main_progress_width) * duration;
    },
  },
};
</script>
