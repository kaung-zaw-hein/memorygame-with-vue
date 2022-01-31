<template>
  <div id="popup1" class="overlay">
          <div class="popup">
            <h2>Congratulations 🎉</h2>
            <a class="close" href=#>×</a>
            <div class="content-1">
              Congratulations you're a winner 🎉🎉
            </div>
            <div class="content-2">
              <p>You made <span id=finalMove> </span> moves </p>
              <p>in <span id=totalTime> </span> </p>
              <p>Rating: <span id=starRating></span></p>
            </div>
            <button id="play-again" onclick="playAgain()">
              Play again 😄
            </button>
          </div>
    </div>
</template>

<script>
export default {

}
</script>

<style>

</style>