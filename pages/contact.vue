<template>
	<div class="contact">
		<h1>
			Contact me
		</h1>
		<p>Email me at <a href="mailto:jon.muller@gmail.com">jon.muller@gmail.com</a> or call me on <a href="tel:0466213376">0466&nbsp;213&nbsp;376</a>.</p>
		<form name="contact" method="POST" data-netlify="true" @submit.prevent="handleSubmit">
			<p>
				<label>Your Name: <input type="text" name="name"/></label>
			</p>
			<p>
				<label>Your Email: <input type="email" name="email"/></label>
			</p>
			<p>
				<label>Message: <textarea name="message"></textarea></label>
			</p>
			<p>
				<button type="submit">Send</button>
			</p>
		</form>
	</div>
</template>

<script>
export default {
	methods: {
		encode(data) {
			return Object.keys(data)
				.map((key) => `${encodeURIComponent(key)}=${encodeURIComponent(data[key])}`)
				.join('&');
		},
		handleSubmit(e) {
			fetch('/', {
				method: 'POST',
				headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
				body: this.encode({
					...this.form
				})
			})
				.then(() => {
					alert('ok good');
				})
				.catch(() => {
					alert('oh no bad');
				});
		}
	}
};
</script>

<style lang="scss"></style>
