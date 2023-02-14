<script>
// @ts-nocheck

    import {disQuestions} from './questions';

    let questions = JSON.parse(localStorage.getItem('discussion'));
    if (!questions) {
        questions = disQuestions;
        localStorage.setItem('discussion', JSON.stringify(questions));
    }

    const save = () => {
        localStorage.setItem('discussion', JSON.stringify(questions));
    }

</script>

<main>
    <h1>Discussion Questions</h1>
    <p id="instructions">
        Fill out these discussion questions to establish your intentions for creating Atomic Habits. Questions taken from Atomic Habits.
    </p>
    {#each questions as question, i}
        <div class="card question">
            <label for={i} class="form-label question">{question.question}</label>
            <div class="input-group">
                <textarea on:keyup={save} bind:value={question.answer} id={i} class="form-control" aria-label="With textarea"></textarea>
            </div>
        </div>
    {/each}
</main>
<style>
    main {
        margin: auto;
        width: 80%;
    }
    textarea {
        resize: none;
    }
    .question {
        text-align: left;
        margin-bottom: 10px;
    }
    #instructions {
        padding: 10px;
        text-align: left;
    }
</style>