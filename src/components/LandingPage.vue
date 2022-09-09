<template>
  <div class="container-fluid content bg-wrapper">
    <section class="container-fluid content content--intro p-3 mb-3">
      <h1 class="display-1 p-4 mb-4">This doesn't need to be you.</h1>
      <div class="container-fluid content img-container p-3 mb-3">
        <figure class="figure text-center">
          <img src="../assets/img/drowning.jpg" class="figure-img img-fluid rounded" alt="A person struggling with mental health issues">
          <figcaption class="figure-caption"><em>Feel like you're drowning?</em></figcaption>
        </figure>
      </div>

    </section>

    <section class="container-fluid content content--call">
      <span>
        <img src="../assets/icon/chevron-double-right.svg" class="p-3 mb-3" alt="Chevron Double Right">
        <button class="btn btn-primary btn-lg bg-gradient p-4 mb-4" v-if="isAuthenticated" @click="router.push('/dashboard')">To Dashboard</button>
        <button class="btn btn-primary btn-lg bg-gradient p-4 mb-4" v-else @click="login">Get Started!</button>
        <img src="../assets/icon/chevron-double-left.svg" class="p-3 mb-3" alt="Chevron Double Left">
      </span>

      <div class="container-fluid p-2">
        <hr class="section-break">
      </div>

      <h2 class="display-2 p-4 mt-4 mb-4">
          With MasterMind<br>you can...
      </h2>
    </section>

    <section class="container-fluid content content--get-started p-3 mb-3" id="getStarted">
      <div class="content text-container p-3 mb-3">
        <h3 class="display-3 text-decoration-underline">Track</h3>
        <ul>
          <li>
            <p>Start tracking your mental health with curated exercises recommended by real medical professionals!</p>
          </li>
        </ul>
      </div>
      <div class="container-fluid content img-container p-3 mb-3">
        <figure class="figure text-center">
          <img src="../assets/img/brain.jpg" class="figure-img img-fluid  rounded" alt="The Best Gift is You!">
          <figcaption class="figure-caption"><em>Your brain will thank you!</em></figcaption>
        </figure>
      </div>
    </section>


      <div class="container-fluid p-2">
        <hr class="section-break">
      </div>


    <section class="container-fluid content content--features p-3 mb-3" id="features">
      <div class="content text-container p-3 mb-3">
        <h3 class="display-3 text-decoration-underline">Features</h3>
        <ul>
          <li>
            <p><img src="src/assets/icon/caret-right.svg" alt="Carat Right Icon">
                Create your own tasks, or choose from one of many presets created by mental health professionals</p>
          </li>
          <li>
            <p><img src="src/assets/icon/caret-right.svg" alt="Carat Right Icon">
                Write journal entries to catalogue your daily thoughts and feelings</p>
          </li>
          <li>
            <p><img src="src/assets/icon/caret-right.svg" alt="Carat Right Icon">
                Develop your own gratitude board to begin visualizing what is important to you</p>
          </li>
          <li>
            <p><img src="src/assets/icon/caret-right.svg" alt="Carat Right Icon">
                Align your sleep schedule</p>
          </li>
          <li>
            <p><img src="src/assets/icon/caret-right.svg" alt="Carat Right Icon">
            Record your progress with descriptive statistics and informative data visuals</p>
          </li>
          <li>
            <p><img src="src/assets/icon/caret-right.svg" alt="Carat Right Icon">
                Share your progress on social media</p>
          </li>
        </ul>
      </div>

      <div class="container-fluid content content--features p-3 mb-3">

        <div id="activityCarousel" class="carousel slide carousel-fade" data-bs-ride="true">
          <div class="carousel-indicators">
            <button type="button" data-bs-target="#activityCarousel" data-bs-slide-to="0" class="active" aria-current="true" aria-label="Slide 1"></button>
            <button type="button" data-bs-target="#activityCarousel" data-bs-slide-to="1" aria-label="Slide 2"></button>
            <button type="button" data-bs-target="#activityCarousel" data-bs-slide-to="2" aria-label="Slide 3"></button>
            <button type="button" data-bs-target="#activityCarousel" data-bs-slide-to="3" aria-label="Slide 4"></button>
          </div>

        <div class="carousel-inner">
          <div class="carousel-item active">
            <img src="../assets/img/meditate.jpg" class="d-block w-100 rounded" alt="Meditate!">
            <div class="carousel-caption d-none d-md-block">
              <h4 class="display-4">Meditation</h4>
              <p class="lead">Take time to enjoy a relaxing session of meditation.</p>
            </div>
          </div>

          <div class="carousel-item">
            <img src="../assets/img/naturebreak.jpg" class="d-block w-100 rounded" alt="Take a nature break!">
            <div class="carousel-caption d-none d-md-block">
              <h4 class="display-4">Nature Break</h4>
              <p class="lead">Go out and just enjoy your surroundings.</p>
            </div>
          </div>

          <div class="carousel-item">
            <img src="../assets/img/enjoy.jpg" class="d-block w-100 rounded" alt="Do something you enjoy!">
            <div class="carousel-caption d-none d-md-block">
              <h4 class="display-4">Do Something You Enjoy</h4>
              <p class="lead">Just do something that makes you happy!</p>
            </div>
          </div>

          <div class="carousel-item">
            <img src=../assets/img/talktofriend.jpg class="d-block w-100 rounded" alt="Talk to a friend!">
            <div class="carousel-caption d-none d-md-block">
              <h4 class="display-4">Talk to a Friend</h4>
              <p class="lead">Connect with a friend!</p>
            </div>
          </div>
        </div>

        <button class="carousel-control-prev" type="button" data-bs-target="#activityCarousel" data-bs-slide="prev">
          <span class="carousel-control-prev-icon" aria-hidden="true"></span>
          <span class="visually-hidden">Previous</span>
        </button>
        <button class="carousel-control-next" type="button" data-bs-target="#activityCarousel" data-bs-slide="next">
          <span class="carousel-control-next-icon" aria-hidden="true"></span>
          <span class="visually-hidden">Next</span>
        </button>
      </div>
    </div>
    </section>

    <div class="container-fluid p-2">
        <hr class="section-break">
      </div>

    <section class="container-fluid content content--about p-3 mb-3" id="missionStatement">
      <div class="content text-container p-3 mb-3">
        <h3 class="display-3 text-decoration-underline">Mission</h3>
        <ul>
          <li>
            <p>Dr. Liza Ignatova is a fully licensed and certified practicing pediatrician specializing in adolescent mental health and well-being.</p>
          </li>
        </ul>
       </div>


      <div class="container-fluid content img-container p-3 mb-3">

        <figure class="figure text-center">
          <img src="../assets/img/drliza.jpeg" class="figure-img img-fluid rounded" alt="Dr. Liza Ignatova">
          <figcaption class="figure-caption"><em>Dr. Liza Ignatova</em></figcaption>
        </figure>
      </div>
    </section>
  </div>
</template>

<script>
import { useAuth0 } from '@auth0/auth0-vue';
import router from "../router";

export default {
  name: "LandingPage",

  setup() {
    const {user, isAuthenticated, loginWithRedirect} = useAuth0();

    return {user, isAuthenticated, router,

      login: () => {
          loginWithRedirect()
        },
     }
  }
}

</script>

<style scoped>
  figcaption {
    color: lightyellow;
  }

  .section-break {
    padding: 1.2vw;
    background: lavender;
    border-top: 2.4vw solid lightyellow;
    box-shadow: 1.2vw 2.4vw;
    opacity: 0.75;
  }

  .carousel-inner, .carousel-control-next, .carousel-control-prev {
    border-radius: 16px;
  }

  .carousel-caption {
    color: darkslateblue;
  }
</style>