<script>
  import { fade, slide, scale } from 'svelte/transition';
  import PollStore from '../stores/PollStore.js';
  import { createEventDispatcher } from 'svelte';
  import Button from '../shared/Button.svelte';

  const dispatch = createEventDispatcher();

  let fields = { question: '', answerA: '', answerB: '' };
  let errors = { type: '' };
  // let valid = false;

  const submitHandler = () => {
    if (fields.question.trim().length < 5) {
      errors.type = 'Question cannot be empty';
    } else if (fields.answerA.trim().length < 1) {
      errors.type = 'Answer A cannot be empty';
    } else if (fields.answerB.trim().length < 1) {
      errors.type = 'Answer B cannot be empty';
    } else {
      errors.type = '';

      let poll = { ...fields, votesA: 0, votesB: 0, id: Math.random() };
      // Save poll to store
      PollStore.update(currentPoll => {
        return [poll, ...currentPoll];
      });
      dispatch('add');
    }
  };
</script>

<style>
  form {
    text-align: center;
    color: #666;
    margin: 0 auto;
    width: 30rem;
  }

  .form-field {
    margin: 1.2rem auto;
  }

  input {
    color: #666;
    width: 100%;
    border-radius: 5px;
  }

  label {
    margin: 0.7rem auto;
    text-align: left;
  }

  .errors {
    text-align: center;
    font-weight: bold;
    color: red;
    margin-bottom: 2rem;
  }
</style>

<div in:fade>
  <div class="errors">{errors.type}</div>
  <form on:submit|preventDefault={submitHandler}>
    <div class="form-field">
      <label for="question">Poll Question:</label>
      <input type="text" id="question" bind:value={fields.question} />
    </div>
    <div class="form-field">
      <label for="answer-a">Answer A:</label>
      <input type="text" id="answer-a" bind:value={fields.answerA} />
    </div>
    <div class="form-field">
      <label for="answer-b">Answer B:</label>
      <input type="text" id="answer-b" bind:value={fields.answerB} />
    </div>
    <Button type="secondary">Add poll</Button>
  </form>
</div>
