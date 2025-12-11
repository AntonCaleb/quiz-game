import random
import os

# ----------------------------------------
# Load questions from file
# ----------------------------------------
def load_questions(filename="questions.txt"):
    questions = []
    try:
        with open(filename, "r") as file:
            for line in file:
                parts = line.strip().split("|")
                if len(parts) != 6:
                    continue  # Skip bad lines
                
                question, correct, optA, optB, optC, optD = parts
                questions.append({
                    "question": question,
                    "correct": correct.upper(),
                    "options": {
                        "A": optA,
                        "B": optB,
                        "C": optC,
                        "D": optD
                    }
                })
    except FileNotFoundError:
        print("Error: questions.txt not found.")
    return questions


# ----------------------------------------
# Run the quiz
# ----------------------------------------
def run_quiz(questions):
    random.shuffle(questions)
    score = 0

    print("\n----- QUIZ START -----\n")

    for q in questions:
        print(q["question"])
        for key, option in q["options"].items():
            print(f"{key}) {option}")

        answer = input("Your answer (A/B/C/D): ").upper()

        while answer not in ["A", "B", "C", "D"]:
            print("Invalid input! Try again.")
            answer = input("Your answer (A/B/C/D): ").upper()

        if answer == q["correct"]:
            print("✔ Correct!\n")
            score += 1
        else:
            print(f"✘ Incorrect! Correct answer was {q['correct']}\n")

    print(f"Your final score: {score}/{len(questions)}")
    return score


# ----------------------------------------
# Save score to file
# ----------------------------------------
def save_score(username, score, filename="scores.txt"):
    try:
        with open(filename, "a") as file:
            file.write(f"{username}: {score}\n")
    except Exception as e:
        print("Error saving score:", e)


# ----------------------------------------
# Add a new question
# ----------------------------------------
def add_question(filename="questions.txt"):
    print("\n--- Add a New Question ---")

    question = input("Enter question text: ")

    optA = input("Option A: ")
    optB = input("Option B: ")
    optC = input("Option C: ")
    optD = input("Option D: ")

    correct = input("Correct option (A/B/C/D): ").upper()
    while correct not in ["A", "B", "C", "D"]:
        print("Invalid choice.")
        correct = input("Correct option (A/B/C/D): ").upper()

    try:
        with open(filename, "a") as file:
            file.write(f"{question}|{correct}|{optA}|{optB}|{optC}|{optD}\n")
        print("Question added successfully!\n")
    except Exception as e:
        print("Error writing to file:", e)


# ----------------------------------------
# Display high scores
# ----------------------------------------
def view_scores(filename="scores.txt"):
    print("\n--- High Scores ---")
    
    if not os.path.exists(filename):
        print("No scores yet.\n")
        return

    with open(filename, "r") as file:
        content = file.read().strip()

        if content == "":
            print("No scores yet.\n")
        else:
            print(content + "\n")


# ----------------------------------------
# Main Menu
# ----------------------------------------
def main():
    while True:
        print("------ QUIZ GAME MENU ------")
        print("1. Start Quiz")
        print("2. Add Question")
        print("3. View Scores")
        print("4. Quit")

        choice = input("Choose an option: ")

        if choice == "1":
            username = input("Enter your name: ")
            questions = load_questions()

            if len(questions) == 0:
                print("No questions loaded. Add questions first.\n")
                continue

            score = run_quiz(questions)
            save_score(username, score)

        elif choice == "2":
            add_question()

        elif choice == "3":
            view_scores()

        elif choice == "4":
            print("Goodbye!")
            break
        else:
            print("Invalid choice, try again.\n")


# Run program
if __name__ == "__main__":
    main()
