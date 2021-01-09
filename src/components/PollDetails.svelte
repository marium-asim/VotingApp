<script>

import Card from '../shared/Card.svelte';
import PollStore from '../store/PollStore.js';
import { Button } from 'sveltail';

export let poll;


// reactive values
$: totalVotes = poll.votesA + poll.votesB;
$: percentA = Math.floor(100 / totalVotes * poll.votesA);
$: percentB = Math.floor(100 / totalVotes * poll.votesB);


const handleVote = (option, id) =>
{

        PollStore.update(currentPolls =>
        {
       let copiedPolls = [...currentPolls];
	   let upvotedPoll = copiedPolls.find((poll) => poll.id == id);

	   if (option === 'a')
	   {
		   upvotedPoll.votesA++;
	   }
	   if (option === 'b')
	   {
		   upvotedPoll.votesB++;
	   }

	  return copiedPolls;

        });
	  
};

const handleDelete = (id) => 
{
PollStore.update(currentPolls =>
{
return currentPolls.filter(poll => poll.id != id);
});
};

</script>

<Card>
<div class="poll">
 <h3>{poll.question}</h3>
 <p>Total votes: {totalVotes}</p>

 <div>
     <div class="answer" on:click={() => handleVote('a', poll.id)}>
     <div class="percent percent-a" style="width: {percentA}%"></div>
     <span>{ poll.answerA } ({poll.votesA})</span>
     </div>
      <h3>{poll.answerA}</h3>
  <div>   

<div>
 <div class="answer" on:click={() => handleVote('b', poll.id)}>
     <div class="percent percent-b" style="width: {percentB}%"></div>
     <span>{ poll.answerB } ({poll.votesB}) </span>
     </div>
     <h3>{poll.answerB}</h3>
   </div>  

     <div class="delete">
     <Button label="Delete" size="lg" class="mx-1" colorBg="danger"  on:click={() => handleDelete(poll.id)}/>
     </div>
 </div>
</Card>

 <style>
h3{
    margin: 0 auto;
    color: gray;
}

p{
    margin-top: 6px;
    fonrt-size: 14px;
    color: grey;
    margin-bottom: 30px;
}

.answer{
    background: whitesmoke;
    cursor: pointer;
    margin: 10px auto;
    position: relative;
    
}

.answer:hover
{
    opacity: 0.6;
}

span{
    display: inline-block;
    padding: 10px 20px;
    
}

.percent{
    height: 100%;
    position: absolute;
    box-sizing: border-box;
 
}

.percent-a{
  border-left: 4px solid red;
    background: pink;
}

.percent-b{
    border-left: 4px solid green;
    background: lightgreen;
}

.delete
{
    margin-top: 30px;
    text-align: center;
}
 </style>    


 