<template>
  <section className="py-5 text-center container">
    <div className="row py-lg-5">
      <div className="col-lg-6 col-md-8 mx-auto">
        <h1 className="fw-light">{{ title }}</h1>
        <p className="lead text-muted">{{ description }}</p>
        <p v-if="!user">
          <router-link to="/login" className="btn btn-primary my-2">Login</router-link>
          <router-link to="/register" className="btn btn-secondary my-2">Register</router-link>
        </p>
      </div>
    </div>
  </section>
</template>

<script>
import { computed, ref, watch } from "vue";
import { useStore } from "vuex";

export default {
  name: "Header",
  setup() {
    const title = ref('');
    const description = ref('');
    const store = useStore();
    const user = computed(() => store.state.user);
    title.value = user.value ? '$' + user.value.revenue : 'Welcome';
    description.value = user.value ? 'You have earned this far' : 'Share links to earn money';
    watch(user, () => {
      title.value = user.value ? '$' + user.value.revenue : 'Welcome';
      description.value = user.value ? 'You have earned this far' : 'Share links to earn money';
    });
    return {
      title,
      description,
      user
    }
  }
}
</script>
