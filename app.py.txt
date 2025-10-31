from flask import Flask, render_template, request

app = Flask(__name__)

@app.route("/")
def home():
    return render_template("index.html")

@app.route("/get")
def get_bot_response():
    user_text = request.args.get('msg').lower()

    # Emotion-based logic
    if any(word in user_text for word in ["sad", "low", "down", "upset", "bad"]):
        return "I'm sorry you're feeling this way 😔. Try listening to calming music, journaling, or going for a short walk."
    elif any(word in user_text for word in ["depress", "depression", "hopeless"]):
        return "You’re not alone ❤️. Talking to someone you trust or a counselor can really help."
    elif any(word in user_text for word in ["happy", "good", "great", "joy", "excited"]):
        return "That’s wonderful 😄! Keep doing what makes you feel happy — you're doing amazing!"
    elif any(word in user_text for word in ["angry", "mad", "furious", "rage"]):
        return "Anger is natural 😡. Try deep breathing or listening to calming music — it really helps."
    elif any(word in user_text for word in ["anxious", "nervous", "stress", "panic"]):
        return "Feeling anxious can be hard 😥. Try breathing in for 4 seconds, holding for 4, and exhaling for 4 — it calms your mind."
    elif any(word in user_text for word in ["thanks", "thank you"]):
        return "You're very welcome 💛. I'm always here for you."
    else:
        return "I'm here to listen 🤗. Tell me more about how you’re feeling."

if __name__ == "__main__":
    app.run(debug=True)
