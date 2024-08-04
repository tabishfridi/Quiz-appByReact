#This is the code in which we added a submit button on the last page of questions and on clicking submit buttun i got the score
import React, { useState } from 'react';
import QuestionList from './QuestionList';
import QuizCss from './Quiz.css';

function Quiz() {
  const questions = [
    {
      question: "What is React?",
      options: ['CSS Framework', 'React Library', 'React Framework', 'testing tool'],
      answer: "React Library"
    },
    {
      question: 'User interface developed with React is made of small and isolated pieces of code called ___',
      options: ["Hook", "Component", "Function", "Snippet"],
      answer: "Component"
    },
    {
      question: "What are the two main types of components in React.js?",
      options: ["Class based and functional", "Functional and stateful", "UI and container", "this & that"],
      answer: "Class based and functional"
    },
    {
      question: "Can we update the React elements once they are rendered?",
      options: ["Yes", "No", "May be", "if"],
      answer: "No"
    },
    {
      question: "Applications built with just React usually have a single ___?",
      options: ["Root DOM Node", "Parent Node", "Component", "Constructor"],
      answer: "Root DOM Node"
    },
  ];

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
