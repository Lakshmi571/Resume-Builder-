COURSES = [
    {"id": 1, "name": "Data Science Basics", "skills": ["Python", "Statistics"], "industry": "Data Science"},
    {"id": 2, "name": "Advanced Machine Learning", "skills": ["Machine Learning", "AI"], "industry": "Data Science"},
    {"id": 3, "name": "AI for Business", "skills": ["AI", "Decision Making"], "industry": "Artificial Intelligence"},
    {"id": 4, "name": "Full-Stack Web Development", "skills": ["HTML", "CSS", "JavaScript"], "industry": "Web Development"},
    {"id": 5, "name": "Digital Marketing Essentials", "skills": ["SEO", "Digital Marketing"], "industry": "Marketing"},
    {"id": 6, "name": "Advanced Financial Modeling", "skills": ["Excel", "Finance"], "industry": "Finance"},
    {"id": 7, "name": "Business Analytics", "skills": ["Data Analysis", "Business Intelligence"], "industry": "Business"},
    {"id": 8, "name": "Cybersecurity Fundamentals", "skills": ["Network Security", "Risk Management"], "industry": "Cybersecurity"},
    {"id": 9, "name": "Project Management Professional", "skills": ["PMBOK", "Agile Methodologies"], "industry": "Project Management"},
    {"id": 10, "name": "Machine Learning for Business", "skills": ["Machine Learning", "Business Solutions"], "industry": "Business"},
]

# Function to recommend courses
def recommend_courses(industry=None, skills=None):
    recommendations = []
    if industry:
        recommendations = [course["name"] for course in COURSES if industry.lower() == course["industry"].lower()]
    elif skills:
        for skill in skills:
            for course in COURSES:
                if skill.strip().capitalize() in course["skills"] and course["name"] not in recommendations:
                    recommendations.append(course["name"])
    return recommendations

# Enhanced resume builder
def build_resume():
    print("Welcome to the Enhanced Resume Builder!\n")

    # Collect user details
    name = input("Enter your full name: ").strip()
    alma_mater = input("Enter your alma mater: ").strip()
    education = input("Enter your highest education level (e.g., High School, Bachelor's, Master's): ").strip()
    skills = input("Enter your skills (comma-separated): ").strip().split(",")
    skills = [skill.strip() for skill in skills if skill.strip()]

    desired_industry = input("Enter your desired job industry (e.g., Data Science, Marketing, Finance): ").strip()

    # Optional sections
    work_experience = input("Enter your work experience (press Enter to skip): ").strip()
    achievements = input("Enter your achievements (press Enter to skip): ").strip()

    # Recommend courses
    industry_courses = recommend_courses(industry=desired_industry)
    skill_courses = recommend_courses(skills=skills)

    # Combine course recommendations and remove duplicates
    recommended_courses = list(set(industry_courses + skill_courses))

    # Generate resume content
    resume = f"""
    ----------------------------
    RESUME
    ----------------------------
    Name: {name}
    Alma Mater: {alma_mater}
    Education: {education}
    Skills: {', '.join(skills) if skills else "N/A"}
    Desired Industry: {desired_industry}

    Work Experience: {work_experience if work_experience else "N/A"}
    Achievements: {achievements if achievements else "N/A"}

    Recommended Courses:
    {', '.join(recommended_courses) if recommended_courses else "No courses available for your industry or skills"}
    ----------------------------
    """

    # Display the generated resume
    print("\nGenerated Resume:")
    print(resume)

    # Option to save the resume
    save_option = input("Do you want to save this resume to a file? (yes/no): ").strip().lower()
    if save_option == "yes":
        filename = input("Enter the filename (without extension): ").strip()
        with open(f"{filename}.txt", "w") as file:
            file.write(resume)
        print(f"Resume saved as '{filename}.txt' in the current directory.")

# Chatbot logic
def chat_with_bot():
    print("\nAsk the AI Chatbot a question (type 'exit' to quit):")
    while True:
        message = input("> ").strip().lower()
        if message == "exit":
            print("Goodbye!")
            break

        industries = [
            "data science", "artificial intelligence", "ai", "web development", "marketing",
            "finance", "business", "cybersecurity", "project management", "mobile development", "design", "e-commerce"
        ]
        industry = next((ind for ind in industries if ind in message), None)

        if industry:
            recommendations = recommend_courses(industry=industry)
            if recommendations:
                print(f"I recommend these courses: {', '.join(recommendations)}.")
            else:
                print("I couldn't find any courses matching your industry. Try adjusting your query.")
        elif "skillsfuture" in message:
            print("SkillsFuture is a national initiative to help individuals upskill. Use SkillsFuture credits to attend eligible courses.")
        elif "courses" in message:
            print("SkillsFuture offers courses in:\n- Data Science\n- AI\n- Web Development\n- Marketing\n- Finance\n- Business\n- Cybersecurity\n- Project Management\n- Design\n- E-commerce")
        elif "career advice" in message:
            print("To advance your career, acquire relevant skills, network, and stay updated with the latest industry trends.")
        else:
            print("I'm sorry, I didn't quite understand that. You can ask me about courses, industries, or career advice.")

# Main menu
def main():
    while True:
        print("\n--- AI Chatbot & Enhanced Resume Builder ---")
        print("1. Build Resume")
        print("2. Chat with AI Chatbot")
        print("3. Exit")

        choice = input("Enter your choice: ").strip()

        if choice == "1":
            build_resume()
        elif choice == "2":
            chat_with_bot()
        elif choice == "3":
            print("Thank you for using the program. Goodbye!")
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
# Resume-Builder-
