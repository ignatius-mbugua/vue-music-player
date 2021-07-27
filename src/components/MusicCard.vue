<template>
  <div class="row pt-5">
    <div class="col-sm-12 col-md-6 mx-auto">
      <!-- Card -->
      <div class="card">
        <div class="card-body text-center">
          <!-- Image -->
          <img
            id="music_img"
            src="../assets/images/hey.jpg"
            alt="music-art"
            class="img-fluid"
            width="300"
            height="200"
          />
          <!-- Audio -->
          <audio id="music">
            <source src="" type="audio/ogg" />
            Your broswer doesn't support the audio element
          </audio>
          <!-- Music Info -->
          <h5 class="pt-3"></h5>
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
            <button type="button" class="btn btn-outline-primary float-left">
              <font-awesome-icon icon="step-backward" size="2x" />
            </button>
            <button type="button" class="btn btn-outline-primary">
              <font-awesome-icon icon="play" size="2x" />
            </button>
            <button type="button" class="btn btn-outline-primary float-right">
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
};
</script>
