<script>
import { createEventDispatcher } from 'svelte';
import PollStore from '../store/PollStore.js';
import { Button } from 'sveltail';


  let dispatch = createEventDispatcher();
  let fields = {question: '', answerA: '', answerB: ''};
  let errors= {question: '', answerA: '', answerB: ''};
  let valid= false;
  const submitHandler =()=>
  { 
    valid=true;
    
    //validate question
    if(fields.question.trim().length < 5)
    {
      valid = false;
      errors.question = 'Question must be atleast 5 characters long';

    }

    else
    {
      errors.question = '';
    }

    //validate answerA
     if(fields.answerA.trim().length < 1)
    {
      valid = false;
      errors.answerA = 'Answer A cannot be empty';

    }

    else
    {
      errors.answerA = '';
    }

    //validate answerB
     if(fields.answerB.trim().length < 1)
    {
      valid = false;
      errors.answerB = 'Answer B cannot be empty';
    }

    else
    {
      errors.answerB = '';
    }

    //add new Poll
    if(valid)
    {
      let poll = {...fields, votesA : 0, votesB : 0, id: Math.random()};

      PollStore.update(currentPolls => 
      {
        return [poll, ...currentPolls];
      });

      dispatch('add');
    }
  }
</script>

<form on:submit|preventDefault={submitHandler}>
  <div class="form-field">
  <label for="question">Poll Question: </label>
  <input type="text" id="question" bind:value={fields.question}>
  <div class="error">{ errors.question } </div>
  </div>

  <div class="form-field">
  <label for="answer-a">Answer A:</label>
  <input type="text" id="answer-a" bind:value={fields.answerA}>
  <div class="error">{ errors.answerA } </div>
  </div>

  <div class="form-field">
  <label for="answer-b">Answer B: </label>
  <input type="text" id="answer-b" bind:value={fields.answerB}>
  <div class="error">{ errors.answerB } </div>
  </div>

  <center><Button label="Submit" colorBg="secondary" size="lg" class="mx-1" /></center>

</form>


<style>
form{
    width: 400px;
    margin:0 auto;
    text-align: center;
}

.form-field{
    margin: 18px auto;
}

input{
    width: 100%;
    border-radius: 6px;
    border: 2px solid black;
}

label{
    margin:10px auto;
    text-align: left;
}

.error{
  font-weight: bold;
  color:red;
  font-size: 12px;
}
</style>