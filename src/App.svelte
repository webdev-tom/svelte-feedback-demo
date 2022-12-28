<script>
  import FeedbackList from "./components/FeedbackList.svelte";
  import FeedbackStats from "./components/FeedbackStats.svelte";
  import FeedbackForm from "./components/FeedbackForm.svelte";

  let feedback = [
    {
      id: 1,
      rating: 8,
      text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Mauris ipsum ante, faucibus id tempor ac, blandit nec mauris. Suspendisse eu.'
    },
    {
      id: 2,
      rating: 9,
      text: 'In in leo ante. Nam consequat nisi sit amet metus dapibus fermentum. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Proin non ante placerat, interdum.'
    },
    {
      id: 3,
      rating: 7,
      text: 'Quisque sit amet egestas lectus. Ut nec scelerisque sapien, a egestas enim. Morbi arcu magna, sollicitudin non ex ut, convallis pretium nisl. Duis placerat, sapien vel rhoncus sollicitudin, nunc urna.'
    } 
  ]

  $: count = feedback.length;
  $: average = feedback.reduce((lastVal, {rating}) => lastVal + rating, 0) / feedback.length;

  const deleteFeedback = (e) => {
    const itemId = (e.detail); // e is the event object from dispatcher, detail is our data we passed in, in this case itemId
    feedback = feedback.filter((item) => item.id != itemId);
  }

  const addReview = (e) => {
    const newReview = e.detail;
    feedback = [newReview, ...feedback];
  }
</script>

<main class="container">
  <FeedbackForm on:submit-review={addReview} />
  <FeedbackStats {count} {average} />
	<FeedbackList theFeedback={feedback} on:delete-feedback={deleteFeedback}/>
</main>

