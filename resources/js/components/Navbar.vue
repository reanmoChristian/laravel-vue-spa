<template>
  <nav id="sidebar">
    <ul class="list-unstyled components">
      <li>
        <router-link v-for="link in links" :to="link.link" active-class="active" :key="link.id">
          <span class="item-icon">
            <component v-bind:is="link.icon"></component>
          </span>
          {{ link.name }}
        </router-link>
      </li>
    </ul>
  </nav>
</template>

<script>
import { mapGetters } from 'vuex'
import DashboardIcon from '../icons/DashboardIcon'
import CandidatesIcon from '../icons/CandidatesIcon'
import TasksIcon from '../icons/TasksIcon'
import ProjectsIcon from '../icons/ProjectsIcon'
import CompaniesIcon from '../icons/CompaniesIcon'
import CustomersIcon from '../icons/CustomersIcon'
import SettingsIcon from '../icons/SettingsIcon'

export default {
  components: { CandidatesIcon, DashboardIcon, TasksIcon, ProjectsIcon, CompaniesIcon, CustomersIcon, SettingsIcon },
  data: () => ({
    appName: window.config.appName
  }),

  computed: {
    ...mapGetters({ user: 'auth/user' }),
    links () {
      return [
        { id: 1, name: 'Dashboard', icon: 'DashboardIcon', link: { name: this.user ? 'home' : 'welcome' } },
        { id: 2, name: 'Kandidaten', icon: 'CandidatesIcon', link: { name: this.user ? 'candidates' : 'welcome' } },
        { id: 3, name: 'Aufgaben', icon: 'TasksIcon', link: { name: this.user ? 'tasks' : 'welcome' } },
        { id: 4, name: 'Projekte', icon: 'ProjectsIcon', link: { name: this.user ? 'projects' : 'welcome' } },
        { id: 5, name: 'Unternehmen', icon: 'CompaniesIcon', link: { name: this.user ? 'companies' : 'welcome' } },
        { id: 6, name: 'Kunden', icon: 'CustomersIcon', link: { name: this.user ? 'customers' : 'welcome' } },
        { id: 7, name: 'Einstellungen', icon: 'SettingsIcon', link: { name: this.user ? 'settings.profile' : 'welcome' } }
      ]
    }
  },

  methods: {
    async logout () {
      // Log out the user.
      await this.$store.dispatch('auth/logout')

      // Redirect to login.
      this.$router.push({ name: 'login' })
    }
  }
}
</script>

<style lang="scss" scoped>
.profile-photo {
  width: 2rem;
  height: 2rem;
  margin: -.375rem 0;
}
a,
a:hover,
a:focus {
  color: inherit;
  text-decoration: none;
  transition: all 0.3s;
}

/* ---------------------------------------------------
    SIDEBAR STYLE
----------------------------------------------------- */

.wrapper {
  display: flex;
  width: 100%;
}

#sidebar {
  width: 230px;
  position: fixed;
  top: 0;
  left: 0;
  height: 100vh;
  z-index: 999;
  background: white;
  color: #909CB1;
  transition: all 0.3s;
  border-right: 2px solid #CED4DA;
}

#sidebar ul li a:hover {
  color: #0094ce;
  background: #E7F4FB;
}

#sidebar ul li a.active {
  color: #0094ce;
  font-family: 'Segoe UI Semibold', sans-serif;
  font-size: 16px;
  background: #E7F4FB;
}

#sidebar.active {
  margin-left: 0;
}

#content.active {
  width: calc(100% - 230px);
}

#sidebar .sidebar-header {
  padding: 0 20px;
  background: white;
}

#sidebar ul.components {
  padding: 20px 0;
}

#sidebar ul p {
  color: white;
  padding: 10px;
}

#sidebar ul li a {
  padding: 12px;
  padding-left: 25px;
  font-size: 1em;
  display: block;
}

#sidebar ul li a span.item-icon {
  min-width: 30px;
  margin-left: 10px;
  margin-right: 8px;
  font-size: 20px;
  display: inline-block;
}

a[data-toggle="collapse"] {
  position: relative;
}

/* ---------------------------------------------------
    MEDIAQUERIES
----------------------------------------------------- */

@media (max-width: 1200px) {
  #sidebar {
    margin-left: -250px;
  }

  #sidebar.active {
    margin-left: 0;
  }

  #content {
    width: 100%;
  }

  #content.active {
    width: 100%;
  }

  #sidebarCollapse span {
    display: none;
  }
}

li.active .active-icon-bg {
  fill: #0094ce;
}

li.active .active-icon-border {
  stroke: #0094ce;
}

.notification-bubble {
  height: 18px;
  width: 18px;
  font-size: 12px;
  background: #0094ce;
  display: inline-block;
  color: white;
  text-align: center;
  border-radius: 50%;
  margin-left: 5px !important;
}

</style>
