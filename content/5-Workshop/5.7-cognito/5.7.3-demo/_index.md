---
title: "Demo the Application"
date: 2026-07-21
weight: 3
chapter: false
pre: "<b>5.7.3. </b>"
---

With VPC, RDS, EC2, S3 and Cognito all wired together, this step demonstrates the FlashLearn application actually running end-to-end in the Cloud, before moving on to cleanup.

---

## 1. Register & Sign In (Amazon Cognito)

<!-- Replace with your own screenshot/GIF -->
![Register and sign in flow](/images/5-Workshop/5.7-demo/register-login.gif)

1. Open `http://<EC2-Public-IP>:5000`
2. Click **Sign In** → redirected to Cognito Hosted UI
3. Register a new account → confirm the verification code sent by email
4. Successfully signed in and redirected back to FlashLearn

---

## 2. Create a Flashcard Deck

![Create deck](/images/5-Workshop/5.7-demo/create-deck.gif)

Create a new English–Vietnamese deck and add a few cards.

---

## 3. Attach an Image to a Flashcard (Amazon S3)

![Upload flashcard image](/images/5-Workshop/5.7-demo/upload-image.gif)

Upload an illustration image for a card and confirm it is served back from the S3 bucket (check the image URL / S3 console to prove it isn't stored locally on EC2).

---

## 4. Practice with Spaced Repetition

![Practice mode](/images/5-Workshop/5.7-demo/practice.gif)

Review a deck using the Spaced Repetition scheduler and show the next-review date updating.

---

## 5. Battle Mode (Real-time, SignalR)

![Battle mode](/images/5-Workshop/5.7-demo/battle.gif)

Open two browser sessions (or two accounts), start a battle, and show both sides updating in real time.

---

## 6. Full Walkthrough Video (Optional)

<video controls width="100%" src="/videos/flashlearn-demo.mp4"></video>

---

## Result

After this step, you have proven that:
- The application deployed on EC2 is reachable and functional from a browser
- Authentication via Cognito works end-to-end
- Flashcard images are actually stored in and served from S3
- Real-time features (SignalR) work correctly in the Cloud environment
