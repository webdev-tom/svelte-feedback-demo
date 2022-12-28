<script>
  import { fade, scale } from "svelte/transition";
  import FeedbackItem from "./FeedbackItem.svelte";
  export let theFeedback = [];

  console.log(theFeedback);
</script>

{#each theFeedback as fb (fb.id)}
  <div in:scale out:fade="{{duration: 500}}">
    <FeedbackItem item={fb} on:delete-feedback /> 
    <!-- Above, on:delete-feedback, since event trigger must be added to tag from which it's defined (FeedbackItem). -->

    <!-- The feedback array is in parent (App.svelte), not this component. To "bubble it up" further, we use a technique called "event forwarding". By placing on:delete-feedback without any arguemnts, the dispatcher will be available on the FeedbackList component, giving App.svelte access. -->
  </div>
{/each}