# Fake-Banking-APK-Detection-System
--
import { useState } from "react";
import { CheckCircle, AlertTriangle, Brain, Code, Database, Shield, Zap, Target } from "lucide-react";

export default function DebuggingAssessment() {
  const [currentQuestion, setCurrentQuestion] = useState(0);
  const [answers, setAnswers] = useState({});
  const [showResults, setShowResults] = useState(false);

  const questions = [
    {
      category: "Problem Identification",
      icon: <Target className="w-5 h-5" />,
      question: "When something breaks in your app, what's your very first step?",
      answers: [
        { text: "Try to reproduce the issue consistently", points: 3, explanation: "Excellent! Reproduction is key to systematic debugging." },
        { text: "Check the most recent code changes", points: 2, explanation: "Good approach, but combine with reproduction for better results." },
        { text: "Look at error messages or logs", points: 2, explanation: "Important, but reproduction should come first." },
        { text: "Start changing things to see what fixes it", points: 1, explanation: "This can make problems worse. Try systematic reproduction first." }
      ]
    },
    {
      category: "React Frontend Issues",
      icon: <Code className="w-5 h-5" />,
      question: "Your Dashboard component isn't rendering data. How do you debug this?",
      answers: [
        { text: "Check browser console, then React DevTools for props/state", points: 3, explanation: "Perfect systematic approach for React debugging." },
        { text: "Add console.log statements to see what data is received", points: 2, explanation: "Useful, but DevTools are more efficient for React." },
        { text: "Refresh the page and see if it works", points: 1, explanation: "This might mask the real issue. Investigate the root cause." },
        { text: "Check if the API is returning data correctly", points: 2, explanation: "Good thinking, but check frontend state first." }
      ]
    },
    {
      category: "API Integration",
      icon: <Database className="w-5 h-5" />,
      question: "Your React app can't connect to your Python backend. What's your debugging sequence?",
      answers: [
        { text: "Test API directly with curl/Postman, then check frontend network tab", points: 3, explanation: "Excellent! Isolate layers systematically." },
        { text: "Check CORS settings and network errors in browser", points: 2, explanation: "Good start, but test the API independently first." },
        { text: "Restart both frontend and backend servers", points: 1, explanation: "Might work but doesn't help you understand the root cause." },
        { text: "Look for typos in API endpoints and request formatting", points: 2, explanation: "Important check, but do API testing first." }
      ]
    },
    {
      category: "ML Model Debugging",
      icon: <Brain className="w-5 h-5" />,
      question: "Your threat detection model gives weird results on APK analysis. How do you investigate?",
      answers: [
        { text: "Validate input data format and check preprocessing steps", points: 3, explanation: "Smart! Most ML issues stem from data problems." },
        { text: "Compare results with known good/bad APK examples", points: 2, explanation: "Good validation approach, combine with data checks." },
        { text: "Retrain the model with more data", points: 1, explanation: "Expensive solution. Debug the current model first." },
        { text: "Check model confidence scores and feature importance", points: 2, explanation: "Useful for understanding, but check data pipeline first." }
      ]
    },
    {
      category: "Error Investigation",
      icon: <AlertTriangle className="w-5 h-5" />,
      question: "You get a cryptic error in your Python backend. What's your approach?",
      answers: [
        { text: "Read the full stack trace carefully, then add logging at each step", points: 3, explanation: "Excellent! Stack traces tell you exactly where to look." },
        { text: "Google the error message", points: 2, explanation: "Can be helpful, but understand your specific context first." },
        { text: "Comment out code until the error goes away", points: 1, explanation: "This can work but doesn't help you learn or fix properly." },
        { text: "Add try/catch blocks around suspicious code", points: 2, explanation: "Useful for handling, but find the root cause first." }
      ]
    },
    {
      category: "Dependency Issues",
      icon: <Shield className="w-5 h-5" />,
      question: "You get package conflicts in package.json. What's your strategy?",
      answers: [
        { text: "Read the conflict message, check compatibility, then resolve systematically", points: 3, explanation: "Perfect! Understanding the conflict is key." },
        { text: "Delete node_modules and package-lock.json, then reinstall", points: 2, explanation: "Sometimes works, but better to understand the conflict first." },
        { text: "Use --force flag to override the conflict", points: 1, explanation: "Dangerous! This can break things in subtle ways." },
        { text: "Update all packages to latest versions", points: 1, explanation: "Risky approach that can introduce new incompatibilities." }
      ]
    },
    {
      category: "Testing & Validation",
      icon: <Zap className="w-5 h-5" />,
      question: "How do you verify your fix actually solves the problem?",
      answers: [
        { text: "Test the original failing scenario plus edge cases", points: 3, explanation: "Excellent! Comprehensive verification prevents regressions." },
        { text: "Run the app and check if it works now", points: 2, explanation: "Good start, but test more scenarios to be thorough." },
        { text: "Deploy and see if users report issues", points: 1, explanation: "Too late! Test thoroughly before deployment." },
        { text: "Test only the specific feature that was broken", points: 2, explanation: "Good, but also test related functionality." }
      ]
    }
  ];

  const handleAnswer = (questionIndex, answerIndex) => {
    setAnswers({ ...answers, [questionIndex]: answerIndex });
  };

  const calculateScore = () => {
    const totalPossible = questions.length * 3;
    const earned = Object.entries(answers).reduce((sum, [qIdx, aIdx]) => {
      return sum + questions[parseInt(qIdx)].answers[aIdx].points;
    }, 0);
    return { earned, totalPossible, percentage: Math.round((earned / totalPossible) * 100) };
  };

  const getScoreLevel = (percentage) => {
    if (percentage >= 85) return { level: "Expert Debugger", color: "text-green-400", bg: "bg-green-900/30" };
    if (percentage >= 70) return { level: "Skilled Debugger", color: "text-blue-400", bg: "bg-blue-900/30" };
    if (percentage >= 55) return { level: "Developing Skills", color: "text-yellow-400", bg: "bg-yellow-900/30" };
    return { level: "Needs Practice", color: "text-red-400", bg: "bg-red-900/30" };
  };

  if (showResults) {
    const score = calculateScore();
    const level = getScoreLevel(score.percentage);
    
    return (
      <div className="max-w-4xl mx-auto p-6 bg-gray-50 min-h-screen">
        <div className="bg-gradient-to-r from-blue-600 to-purple-600 text-white rounded-xl p-8 mb-8">
          <h1 className="text-3xl font-bold mb-2">Your Debugging Assessment Results</h1>
          <p className="text-blue-100">Based on your cybersecurity ML project stack</p>
        </div>

        <div className="grid md:grid-cols-3 gap-6 mb-8">
          <div className="bg-white rounded-xl p-6 shadow-lg">
            <h3 className="font-semibold text-gray-700 mb-2">Overall Score</h3>
            <div className="text-3xl font-bold text-blue-600">{score.percentage}%</div>
            <p className="text-gray-500 text-sm">{score.earned}/{score.totalPossible} points</p>
          </div>
          
          <div className={`rounded-xl p-6 shadow-lg ${level.bg} border border-gray-200`}>
            <h3 className="font-semibold text-gray-700 mb-2">Debugging Level</h3>
            <div className={`text-xl font-bold ${level.color}`}>{level.level}</div>
          </div>

          <div className="bg-white rounded-xl p-6 shadow-lg">
            <h3 className="font-semibold text-gray-700 mb-2">Questions Answered</h3>
            <div className="text-3xl font-bold text-purple-600">{Object.keys(answers).length}</div>
            <p className="text-gray-500 text-sm">of {questions.length} questions</p>
          </div>
        </div>

        <div className="bg-white rounded-xl p-6 shadow-lg mb-6">
          <h3 className="text-xl font-bold mb-4 text-gray-800">Question-by-Question Breakdown</h3>
          <div className="space-y-4">
            {questions.map((q, idx) => {
              const answerIdx = answers[idx];
              if (answerIdx === undefined) return null;
              
              const selectedAnswer = q.answers[answerIdx];
              const isOptimal = selectedAnswer.points === 3;
              
              return (
                <div key={idx} className="border border-gray-200 rounded-lg p-4">
                  <div className="flex items-start gap-3 mb-2">
                    {q.icon}
                    <div className="flex-1">
                      <h4 className="font-semibold text-gray-800">{q.category}</h4>
                      <p className="text-gray-600 text-sm">{q.question}</p>
                    </div>
                    <div className={`px-3 py-1 rounded-full text-sm font-medium ${
                      isOptimal ? 'bg-green-100 text-green-800' : 
                      selectedAnswer.points === 2 ? 'bg-yellow-100 text-yellow-800' : 
                      'bg-red-100 text-red-800'
                    }`}>
                      {selectedAnswer.points}/3
                    </div>
                  </div>
                  <div className="ml-8">
                    <p className="text-gray-700 font-medium mb-1">Your answer: {selectedAnswer.text}</p>
                    <p className="text-gray-600 text-sm">{selectedAnswer.explanation}</p>
                  </div>
                </div>
              );
            })}
          </div>
        </div>

        <div className="bg-gradient-to-r from-gray-800 to-gray-700 text-white rounded-xl p-6">
          <h3 className="text-xl font-bold mb-4">Personalized Recommendations</h3>
          <div className="grid md:grid-cols-2 gap-6">
            <div>
              <h4 className="font-semibold text-blue-300 mb-3">For Your Tech Stack:</h4>
              <ul className="space-y-2 text-gray-300">
                <li>• Use React DevTools for component state debugging</li>
                <li>• Set up structured logging in your Python backend</li>
                <li>• Test API endpoints independently before frontend integration</li>
                <li>• Validate ML model inputs at each pipeline stage</li>
              </ul>
            </div>
            <div>
              <h4 className="font-semibold text-purple-300 mb-3">Next Steps:</h4>
              <ul className="space-y-2 text-gray-300">
                <li>• Create debugging checklists for common scenarios</li>
                <li>• Set up error monitoring (Sentry, LogRocket)</li>
                <li>• Build health check endpoints for your services</li>
                <li>• Document your debugging wins for future reference</li>
              </ul>
            </div>
          </div>
        </div>

        <button 
          onClick={() => {setShowResults(false); setCurrentQuestion(0); setAnswers({});}}
          className="mt-6 bg-blue-600 hover:bg-blue-700 text-white px-8 py-3 rounded-lg font-medium transition-colors"
        >
          Take Assessment Again
        </button>
      </div>
    );
  }

  const currentQ = questions[currentQuestion];
  const progress = ((currentQuestion + 1) / questions.length) * 100;
  const canProceed = answers[currentQuestion] !== undefined;

  return (
    <div className="max-w-3xl mx-auto p-6 bg-gray-50 min-h-screen">
      <div className="bg-gradient-to-r from-blue-600 to-purple-600 text-white rounded-xl p-8 mb-8">
        <h1 className="text-3xl font-bold mb-2">Debugging Skills Assessment</h1>
        <p className="text-blue-100">Tailored for full-stack ML cybersecurity projects</p>
      </div>

      <div className="mb-8">
        <div className="flex justify-between text-sm text-gray-600 mb-2">
          <span>Question {currentQuestion + 1} of {questions.length}</span>
          <span>{Math.round(progress)}% Complete</span>
        </div>
        <div className="w-full bg-gray-200 rounded-full h-3">
          <div 
            className="bg-gradient-to-r from-blue-500 to-purple-500 h-3 rounded-full transition-all duration-500"
            style={{ width: `${progress}%` }}
          ></div>
        </div>
      </div>

      <div className="bg-white rounded-xl shadow-lg p-8 mb-6">
        <div className="flex items-center gap-3 mb-6">
          {currentQ.icon}
          <div>
            <span className="text-sm font-medium text-purple-600 uppercase tracking-wide">{currentQ.category}</span>
            <h2 className="text-xl font-bold text-gray-800">{currentQ.question}</h2>
          </div>
        </div>

        <div className="space-y-3">
          {currentQ.answers.map((answer, idx) => (
            <label 
              key={idx}
              className={`block p-4 border-2 rounded-lg cursor-pointer transition-all hover:shadow-md ${
                answers[currentQuestion] === idx 
                  ? 'border-blue-500 bg-blue-50' 
                  : 'border-gray-200 hover:border-gray-300'
              }`}
            >
              <div className="flex items-center gap-3">
                <input
                  type="radio"
                  name={`question_${currentQuestion}`}
                  checked={answers[currentQuestion] === idx}
                  onChange={() => handleAnswer(currentQuestion, idx)}
                  className="w-4 h-4 text-blue-600"
                />
                <span className="text-gray-800 font-medium">{answer.text}</span>
              </div>
            </label>
          ))}
        </div>
      </div>

      <div className="flex justify-between items-center">
        <button 
          onClick={() => setCurrentQuestion(Math.max(0, currentQuestion - 1))}
          disabled={currentQuestion === 0}
          className="px-6 py-2 bg-gray-200 text-gray-600 rounded-lg font-medium disabled:opacity-50 disabled:cursor-not-allowed hover:bg-gray-300 transition-colors"
        >
          Previous
        </button>

        <div className="flex gap-2">
          {questions.map((_, idx) => (
            <div
              key={idx}
              className={`w-3 h-3 rounded-full transition-colors ${
                idx === currentQuestion ? 'bg-blue-500' : 
                answers[idx] !== undefined ? 'bg-green-500' : 'bg-gray-300'
              }`}
            />
          ))}
        </div>

        {currentQuestion === questions.length - 1 ? (
          <button 
            onClick={() => setShowResults(true)}
            disabled={!canProceed}
            className="px-8 py-2 bg-green-600 text-white rounded-lg font-medium disabled:opacity-50 disabled:cursor-not-allowed hover:bg-green-700 transition-colors"
          >
            View Results
          </button>
        ) : (
          <button 
            onClick={() => setCurrentQuestion(currentQuestion + 1)}
            disabled={!canProceed}
            className="px-6 py-2 bg-blue-600 text-white rounded-lg font-medium disabled:opacity-50 disabled:cursor-not-allowed hover:bg-blue-700 transition-colors"
          >
            Next
          </button>
        )}
      </div>

      {!canProceed && (
        <p className="text-center text-gray-500 text-sm mt-4">
          Please select an answer to continue
        </p>
      )}
    </div>
  );
}
