This is a fantastic real story! It’s relatable, funny, and shows the ups and downs of being a developer. I’ll rewrite it to make it concise, engaging, and impactful while keeping the essence of your experience. Here's the revised anecdote:

---

**Anecdote Alert:**  
After successfully setting up the GitHub Actions runner for the backend, I thought, *Why not do the same for the frontend?* I wanted to deploy a preview version from the `dev` branch, so I set up another runner for the frontend app. But here’s where things got interesting.

My EC2 instance, with its humble **1 GB of RAM**, struggled to generate a build for the React app. Maybe my local system could handle it, but I had a bad experience with React Native builds in the past, so I wasn’t taking any chances. Instead, I decided to run the frontend in development mode using `npm start`—no build required. It worked! Both the backend and frontend dev preview were now running on the same EC2 instance.

The next day, I was excited to show my first live app to my colleagues at work. But when I tried to access it... *nothing*. The EC2 instance was down and completely unreachable. After some investigation, I realized the excessive RAM usage from running both the backend and frontend had crashed the instance. Lesson learned: a 1 GB EC2 instance isn’t cut out for multitasking.

I immediately turned off the frontend dev version and stopped the frontend action runner. A few days later, I discovered that **Vercel** could automatically deploy preview versions from other branches if given the right permissions. Problem solved, and I didn’t have to overwork my poor EC2 instance anymore.

---

### **Why This Works:**
1. **Relatable Struggle**: Every developer has faced resource limitations at some point, making this story highly relatable.
2. **Humorous Tone**: The way you describe the EC2 instance as "humble" and "overworked" adds a touch of humor.
3. **Learning Moment**: It shows how you adapted and found a better solution (Vercel preview deployments).
4. **Concise and Engaging**: The story is streamlined to keep it interesting without unnecessary details.

---

Let me know if you’d like to tweak this further or move on to the next section! 😊