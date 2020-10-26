<template>
  <Layout>
    <section class="about">
      <!-- PAGE HEADER -->
      <div class="pageHeader">
        <h3 class="title">TAI COLLECTIVE</h3>
        <i class="blurb"
          >Tai Collective is a group of Māori & Pasifika creatives and
          entrepreneurs dedicated to mentoring young people in the creative
          fields that they are experts in.
          <br />
          <br />
          Tai Collective teams can develop client projects in areas of:
        </i>
        <br />
        <br />
        <i class="blurb">
          <ul class="blurb">
            <li class="blurb">web development</li>
            <li class="blurb">app development</li>
            <li class="blurb">game development</li>
            <li class="blurb">music production</li>
            <li class="blurb">audio production</li>
            <li class="blurb">photo production</li>
            <li class="blurb">video production</li>
            <li class="blurb">art and design</li>
            <li class="blurb">toi Māori</li>
            <li class="blurb">puoro Māori</li>
          </ul>
          <br />
          Our aim is to give young Māori & Pasifika the opportunity to gain
          real-world experience working on real-world projects inspiring them
          into innovative, creative and entrepreneurial pursuits, so that they
          can live rich, fulfilling lives.
        </i>
      </div>

      <!-- MENTORS -->
      <section class="row">
        <h3 class="title">MENTORS</h3>
        <div class="flexbox">
          <article
            @click="goTo()"
            class="people"
            v-for="mentor in mentors"
            :key="mentor.id"
          >
            <div>
              <!-- PROFILE PIC -->
              <g-image
                class="profilePic"
                :src="mentor.profilePic"
                :alt="mentor.name + '\'s profile picture'"
                width="50"
              ></g-image>
              <!-- NAME -->
              <p style="text-align: center">
                {{ mentor.name.toUpperCase() }}
              </p>
              <!-- CONTACTS -->
              <div class="contacts">
                <span style="font-size: 20px; color: white">
                  <a :href="'mailto:' + mentor.email">
                    <font-awesome
                      :icon="['far', 'envelope']"
                      class="clickable"
                    />
                  </a>
                </span>
              </div>
              <!-- SKILLS -->
              <div
                class="skillBox"
                v-for="(skill, name) in mentor.skills"
                :key="skill.id"
              >
                <div>{{ name }}</div>
                <div><span v-for="i in skill" :key="i.id">🔥</span></div>
              </div>
            </div>
          </article>
        </div>
      </section>

      <!-- RANGATAHI -->
      <section class="row">
        <h3 class="title">RANGATAHI</h3>
        <div class="flexbox">
          <article
            @click="goTo()"
            class="people"
            v-for="student in students"
            :key="student.id"
          >
            <div>
              <g-image
                class="profilePic"
                :src="student.profilePic"
                :alt="student.name + '\'s profile picture'"
                width="50"
              ></g-image>
              <p style="text-align: center">
                {{ student.name.toUpperCase() }}
              </p>
            </div>
          </article>
        </div>
      </section>
    </section>
  </Layout>
</template>

<page-query>
query Projects {
  projects: allProject {
    edges {
      node { 
        id
        path
        title
        year
        thumbnail
        categories
      }
    }
  }
}
</page-query>

<script>
import ProjectMeta from "@/components/ProjectMeta";

export default {
  components: {
    ProjectMeta,
  },
  data() {
    return {
      mentors: [
        {
          name: "ian tairea",
          profilePic: "uploads/ian.png",
          email: "i.tairea@taiwananga.co.nz",
          skills: {
            code: 5,
            business: 4,
            design: 3,
          },
          social: {
            linkedin: "",
            github: "",
          },
        },
        {
          name: "taipari waaka",
          profilePic: "uploads/taipari.jpg",
          email: "taipariwaaka@gmail.com",
          skills: {
            "music production": 5,
          },
          social: {
            linkedin: "",
            github: "",
          },
        },
      ],
      students: [
        {
          name: "tai wānanga",
          profilePic: "uploads/tw-logo.png",
        },
      ],
    };
  },
  metaInfo: {
    titleTemplate: require("../data/theme.json").site_name,
  },
  methods: {
    goTo(event, route) {
      const distanceScrolled = window.pageYOffset;
      const elementPosition = event.target.getBoundingClientRect().top;
      const totalOffset = distanceScrolled + elementPosition;
      const finalPosition = totalOffset - 167;

      // Scroll window so that the thumbnail is 12rem from the
      // top of the browser window, this will make a seamless transition.
      window.scrollTo({ top: finalPosition, behavior: "smooth" });

      // Now, navigate to the project page
      setTimeout(() => {
        this.$router.push(route);
      }, 450);
    },
  },
};
</script>

<style lang="scss" scoped>
.pageHeader {
  width: 80vw;
  margin: 0 auto 50px auto;

  @media (min-width: 1200px) {
    width: 40%;
  }
}

.title {
  text-align: center;
  letter-spacing: 2px;
  margin: 25px;
}

.blurb {
  font-weight: 400;
  line-height: 25px;
  font-size: 14px;
  margin: 0;
}

.row {
  margin: 100px 0;
}

.people {
  margin: 50px;
  // border: solid red 2px;

  .profilePic {
    width: 200px;
    height: 200px;
    object-fit: cover;
    border-radius: 50%;
  }
}

.flexbox {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  width: 100%;
  flex-direction: row;
  // border: 2px solid yellow;

  @media (max-width: 500px) {
    flex-direction: column;
    align-items: center;
  }
}

.skillBox {
  display: flex;
  justify-content: space-between;
}

.contacts {
  text-align: center;
  margin: 10px;
}

.clickable {
  cursor: pointer;
}
</style>
