### **The Journey of Building BattleCompare: From Idea to a Stock Market Learning Platform**

It all started on a lazy weekend with my two friends, Ranjit (aka *Manager*) and Pradip. We were hanging out in my personal workspace—a small room where I spend most of my time tinkering with code. My laptop, as usual, was on, and we were just having a good time (you know what I mean 😉). Out of nowhere, Manager searched for *HigherLower* on Google and opened the website. The vibe of the site, especially the background image, instantly drew us in. We started playing the guessing game, and before we knew it, we were hooked.

That’s when the idea hit me: *What if I could build something similar and surprise my friends by next weekend?* I started brainstorming ideas for comparison games. Here are some of the ideas I came up with:
- **Social Media Influencers**: Guess who has more followers—Person A or Person B?
- **Amazon Product Prices**: Compare the prices of random items on Amazon.
- **Movie Ratings**: Guess which movie has a higher IMDb or Rotten Tomatoes score.
- **Sports Stats**: Compare player stats like goals, assists, or points.
- **Tech Gadgets**: Guess which gadget is more expensive or has better specs.

But out of all these ideas, I finally decided to go with the **stock market**. Why? Because even I’m a beginner in this field, and I wanted to learn more about it while building something useful for the community. That’s how **BattleCompare** was born—a platform where beginners like me could learn about the stock market in a fun, interactive way.

---

### **The Early Days: React, Node.js, and a Lot of Chai 🚬**

Yes, I’m a chai lover, and my journey with BattleCompare began with countless cups of chai and a simple React app powered by a Node.js Express backend. But my first big challenge wasn’t coding—it was finding a reliable, free stock data provider. I spent hours exploring options like **Financial Modeling Prep (FMP)**, **Alpha Vantage**, **Polygon**, and even the **NSE official website**. After weighing the pros and cons, I decided to go with FMP. Here’s why:
- **Higher API Rate Limits**: Even in the freemium model, FMP offered generous API rate limits, which was perfect for a beginner-friendly app.
- **Easy-to-Start API Guide**: FMP’s documentation was beginner-friendly, with clear examples and sample data to help me get started quickly.

**Behind the Scenes:**  
At the time, I didn’t know about Yahoo Finance, so I started building the game with NASDAQ-listed companies only. It wasn’t until later that I discovered FMP’s free subscription didn’t support Indian companies. This limitation led to the first version of BattleCompare being focused solely on U.S. stocks. But I didn’t let that stop me—I kept working on improving the gameplay and user experience. Recently, I integrated **Yahoo Finance** to add Indian companies, making the game more inclusive and relevant for a global audience.

---

### **First Deployment: NASDAQ Version Goes Live**

On **15th December 2024**, I finally deployed the first version of BattleCompare. It was a proud moment—the NASDAQ version of the game was live! The frontend was hosted on **Vercel**, and the backend was running on **Render.com**. Everything seemed to be working perfectly... until I noticed a small but frustrating issue.

**Behind the Scenes:**  
Render’s free tier doesn’t keep web services always running. On the first request, it takes around **30 to 45 seconds** to "wake up" the server. For a game that’s supposed to be fast and interactive, this was a dealbreaker. I knew I had to find a better solution.

---

### **Moving to AWS EC2: A New Challenge**

After some research, I decided to move the backend to **AWS EC2 Free Tier** with an Ubuntu instance. This solved the "wake-up" delay issue, but it came with its own set of challenges. Now, I had to manually deploy updates to the server, which felt like a step backward. I missed the convenience of auto-deployment that Render and Vercel provided.

That’s when I realized it was time to dive into **CI/CD (Continuous Integration and Continuous Deployment)**. I had heard about it before but never had the chance to implement it. Now, it became a necessity.

---

### **Learning CI/CD: The Game-Changer**

I started exploring CI/CD tools and eventually settled on **GitHub Actions**. The idea of automating deployments was exciting, but setting it up on a self-hosted runner was a whole new adventure. Here’s how I did it:
1. **Set Up a Self-Hosted Runner**: I configured a GitHub Actions runner on my AWS EC2 instance to handle deployments.
2. **Automated Backend Deployment**: Every time I pushed code to the main branch, the runner would automatically deploy the changes to the EC2 instance.
3. **Kept Vercel for Frontend**: Since Vercel was doing a fantastic job with the frontend, I left it as is. It was already handling auto-deployment seamlessly.

**Anecdote Alert:**  
After successfully setting up the GitHub Actions runner for the backend, I thought, *Why not do the same for the frontend?* I wanted to deploy a preview version from the `dev` branch, so I set up another runner for the frontend app. But here’s where things got interesting.

My EC2 instance, with its humble **1 GB of RAM**, struggled to generate a build for the React app. Maybe my local system could handle it, but I had a bad experience with React Native builds in the past, so I wasn’t taking any chances. Instead, I decided to run the frontend in development mode using `npm start`—no build required. It worked! Both the backend and frontend dev preview were now running on the same EC2 instance.

The next day, I was excited to show my first live app to my colleagues at work. But when I tried to access it... *nothing*. The EC2 instance was down and completely unreachable. After some investigation, I realized the excessive RAM usage from running both the backend and frontend had crashed the instance. Lesson learned: a 1 GB EC2 instance isn’t cut out for multitasking.

I immediately turned off the frontend dev version and stopped the frontend action runner. A few days later, I discovered that **Vercel** could automatically deploy preview versions from other branches if given the right permissions. Problem solved, and I didn’t have to overwork my poor EC2 instance anymore.

---

### **Why This Move Was Worth It**
- **No More Delays**: The EC2 instance kept the backend running 24/7, eliminating the "wake-up" delay.
- **Automated Workflow**: CI/CD made deployments faster and less error-prone.
- **Learning Opportunity**: I gained hands-on experience with AWS, GitHub Actions, and CI/CD—skills that are invaluable for any developer.

---

### **The Shift to Next.js: Leveling Up the Platform**

As BattleCompare grew, I realized I needed a more robust framework to handle the increasing complexity. That’s when I discovered **Next.js**. The idea of server-side rendering, built-in API routes, and simplified routing was too good to pass up. But migrating from React to Next.js wasn’t a walk in the park.

**Behind the Scenes:**  
I spent an entire weekend rewriting the app. At one point, I accidentally deleted a crucial component and had to rewrite it from scratch. It was frustrating, but it also forced me to understand the code at a deeper level. The switch to Next.js paid off—faster load times, better SEO, and a more streamlined development process.

---

### **Technical Stories: S3, Points, and Shareable URLs**

One of the most interesting technical challenges was optimizing the loading of stock logos. Initially, I was fetching them directly from the APIs, which slowed down the app. After some research, I decided to move the logos to **Amazon S3**. Not only did this improve performance, but it also reduced costs. 

**Fun Fact:**  
I initially thought S3 would be complicated to set up, but it turned out to be surprisingly straightforward. The hardest part was writing a script to batch-upload all the logos. I may or may not have accidentally uploaded the same logo 50 times before getting it right.

Another exciting addition was the **point system**. I wanted to make the game more competitive, so I spent days fine-tuning the scoring logic. For example, if you guess correctly on the first try, you get 10 points. If it takes you two tries, you get 5 points. It’s simple but effective.

Right now, I’m working on making each trivia shareable. The idea is to generate unique URLs for each game so users can challenge their friends directly. It’s still a work in progress, but I’m excited about the potential for virality.

---

### **The Evolution of My Vision**

Initially, I envisioned BattleCompare as a platform with multiple types of games, blogs, and even my portfolio. But as I worked on it, I realized there was a bigger opportunity to create something truly valuable for beginners in the stock market. 

**Anecdote Alert:**  
I remember talking to a friend who had just started investing. He told me how overwhelming it felt to understand stock trends and make informed decisions. That conversation was a turning point for me. I decided to focus BattleCompare on helping users learn and test their knowledge through interactive games.

---

### **Lessons Learned: More Than Just Code**

Building BattleCompare has been an incredible learning experience. I’ve picked up new technical skills like setting up CI/CD pipelines, working with Next.js, and optimizing storage with S3. But more importantly, I’ve learned the value of perseverance and adaptability.

**Behind the Scenes:**  
There were moments when I felt stuck, like when I couldn’t figure out how to structure the database or when a bug kept crashing the app. But every time I solved a problem, it felt like a small victory. I also learned that projects rarely turn out exactly as planned—and that’s okay. What matters is staying focused on the end goal and being willing to pivot when necessary.

---

### **What’s Next for BattleCompare?**

I’m excited about the future of BattleCompare. Here are some features I’m currently working on or planning to add:
- **Stock Trend Charts**: To help users visualize trends and understand why one stock might be performing better than another.
- **Multiplayer Mode**: So users can compete against friends or random opponents in real-time.
- **Portfolio Simulation**: A virtual portfolio where users can apply what they’ve learned in a risk-free environment.

---

### **Try It Out and Share Your Feedback**

If you’re curious to see how BattleCompare works, head over to [insert link] and give it a try! I’d love to hear your feedback and suggestions. And if you’re a developer working on your own project, don’t be afraid to start small and iterate—you never know where your journey might take you.

---

### **Final Thoughts**

Building BattleCompare has been one of the most rewarding experiences of my life. It’s taught me that with a little curiosity, a lot of hard work, and a willingness to learn, you can turn an idea into something real. Whether you’re a developer, a stock market enthusiast, or just someone with a dream, I hope my journey inspires you to take that first step.

Thanks for reading, and happy battling! 🚀
