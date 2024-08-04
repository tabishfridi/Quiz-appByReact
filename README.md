#This is the code in which we added a submit button on the last page of questions and on clicking submit buttun i got the score


  const [currentQuestionIndex, setCurrentQuestionIndex] = useState(0);
  const [currentAnswer, setCurrentAnswer] = useState(null);
  const [score, setScore] = useState(0);
  const [isQuizFinished, setIsQuizFinished] = useState(false);

  const handleClick = (option) => {
    setCurrentAnswer(option);
    if (option === questions[currentQuestionIndex].answer) {
      setScore(score + 1);
    }
  };

  const handleNextQuestion = () => {
    if (currentQuestionIndex < questions.length - 1) {
      setCurrentQuestionIndex(currentQuestionIndex + 1);
      setCurrentAnswer(null);
    } else {
      setIsQuizFinished(true);
    }
  };

  return (
    <div>
      {isQuizFinished ? (
        <div>Your Score is {score}</div>
      ) : (
        <div>
          <QuestionList 
            question={questions[currentQuestionIndex].question}
            options={questions[currentQuestionIndex].options}
            handleClick={handleClick}
            currentAnswer={currentAnswer}
          />
          {currentQuestionIndex < questions.length - 1 ? (
            <button
              disabled={currentAnswer == null}
              className={currentAnswer === null ? 'button-disable' : 'button'}
              onClick={handleNextQuestion}
            >
              Next Question
            </button>
          ) : (
            <button
              disabled={currentAnswer == null}
              className={currentAnswer === null ? 'button-disable' : 'button'}
              onClick={handleNextQuestion}
            >
              Submit
            </button>
          )}
        </div>
      )}
    </div>
  );
}

export default Quiz;
