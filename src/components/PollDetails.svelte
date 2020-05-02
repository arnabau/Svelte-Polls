<script>
  import { fade, slide, scale } from 'svelte/transition';
  import Card from '../shared/Card.svelte';
  import Button from '../shared/Button.svelte';
  import PollStore from '../stores/PollStore.js';

  export let poll;

  // reactive values
  $: totalVotes = poll.votesA + poll.votesB;
  $: percentA = Math.floor((100 / totalVotes) * poll.votesA);
  $: percentB = Math.floor((100 / totalVotes) * poll.votesB);

  const handleVote = (option, id) => {
    PollStore.update(currentPolls => {
      let copiedPolls = [...currentPolls];
      let upvotedPoll = copiedPolls.find(poll => poll.id == id);

      if (option === 'a') {
        upvotedPoll.votesA++;
      } else if (option === 'b') {
        upvotedPoll.votesB++;
      }

      return copiedPolls;
    });
  };

  const handleDelete = id => {
    PollStore.update(currentPolls => {
      return currentPolls.filter(poll => poll.id != id);
    });
  };
</script>

<style>
  .poll {
    margin: 1rem;
  }

  h3 {
    margin: 0 auto;
    color: #555;
  }

  p {
    margin-top: 0.5rem;
    font-size: 0.9rem;
    color: #aaa;
    margin-bottom: 1.5rem;
  }

  .answer {
    background: #fafafa;
    cursor: pointer;
    margin: 0.9rem auto;
    position: relative;
  }

  .answer:hover {
    opacity: 0.6;
  }

  span {
    display: inline-block;
    padding: 1rem 1rem;
  }

  .percent {
    height: 100%;
    /* position: absolute; */
    box-sizing: border-box;
  }

  .percent-a {
    border-left: 4px solid #d91b42;
    background: rgba(217, 27, 66, 0.2);
  }

  .percent-b {
    border-left: 4px solid #45c496;
    background: rgba(69, 196, 150, 0.2);
  }

  .delete {
    margin-top: 1.5rem;
    text-align: right;
  }
</style>

<Card>
  <div class="poll">
    <h3>{poll.question}</h3>
    <p>Total votes: {totalVotes}</p>
    <div class="answer" on:click={() => handleVote('a', poll.id)}>
      <div class="percent percent-a" style="width: {percentA}%">
        <span>{poll.answerA} ({poll.votesA})</span>
      </div>
    </div>
    <div class="answer" on:click={() => handleVote('b', poll.id)}>
      <div class="percent percent-b" style="width: {percentB}%">
        <span>{poll.answerB} ({poll.votesB})</span>
      </div>
    </div>
    <div class="delete" out:scale|local>
      <Button flat="true" on:click={() => handleDelete(poll.id)}>Delete</Button>
    </div>
  </div>
</Card>
