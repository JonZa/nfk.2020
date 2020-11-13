<template>
	<div>
		<div class="content">
			<h1>I'm Jon Muller</h1>
			<p>
				I've been building user interfaces<br class="soft" />
				for over 20 years.
			</p>
			<p>
				I've been described as:<br />
				<strong>“a frontend development genius”</strong><br class="soft" />
				by a head of engineering,<br  />
				<strong>“great at simplifying complex problems”</strong><br class="soft" />
				by a client, and<br />
				<strong>“the best manager I have worked for”</strong><br class="soft" />
				by a teammate.
			</p>
			<p>
				I'm in Sydney, Australia,<br class="soft" />
				and I'm looking for work.
			</p>
			<p>
				Email me at <a href="mailto:jon.muller@gmail.com">jon.muller@gmail.com</a><br class="soft" />
				or <nuxt-link to="/game">read more</nuxt-link> about me.
			</p>
			<!-- <main>
        <div class="post" v-for="post in sortedPosts" :key="post.id">
          <h3>
            <a :href="`blog/${post.slug}`">{{ post.title.rendered }}</a>
          </h3>
          <small>{{ post.date | dateformat }}</small>
          <div v-html="post.excerpt.rendered"></div>
          <a :href="`blog/${post.slug}`" class="readmore slide">Read more ⟶</a>
        </div>
      </main>
      <aside>
        <h2 class="tags-title">Tags</h2>
        <div class="tags-list">
          <ul>
            <li
              @click="updateTag(tag)"
              v-for="tag in tags"
              :key="tag.id"
              :class="[tag.id === selectedTag ? activeClass : '']"
            >
              <a>{{ tag.name }}</a>
              <span v-if="tag.id === selectedTag">✕</span>
            </li>
          </ul>
        </div>
      </aside> -->
		</div>
	</div>
</template>

<script>
export default {
	components: {},
	data() {
		return {
			selectedTag: null,
			activeClass: 'active'
		};
	},
	computed: {
		posts() {
			return this.$store.state.posts;
		},
		tags() {
			return this.$store.state.tags;
		},
		sortedPosts() {
			if (!this.selectedTag) return this.posts;
			return this.posts.filter(el => el.tags.includes(this.selectedTag));
		}
	},
	created() {
		this.$store.dispatch('getPosts');
	},
	methods: {
		updateTag(tag) {
			if (!this.selectedTag) {
				this.selectedTag = tag.id;
			} else {
				this.selectedTag = null;
			}
		}
	}
};
</script>

<style lang="scss" scroped>
@import '@/assets/mixins.scss';
br.soft {
	@include bp(desktop) {
		display: none;
	}
}
</style>
