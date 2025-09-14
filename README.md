[deepseek_python_20250914_2f3345.py](https://github.com/user-attachments/files/22324285/deepseek_python_20250914_2f3345.py)
import tweepy
import pandas as pd
from datetime import datetime
import matplotlib.pyplot as plt

class SocialMediaEmotionMonitor:
    def __init__(self, analyzer):
        self.analyzer = analyzer
        self.results = []
    
    def analyze_tweets(self, query, count=100):
        """Analyze tweets for a given query"""
        # Note: You need Twitter API credentials for this
        # auth = tweepy.OAuthHandler(API_KEY, API_SECRET)
        # auth.set_access_token(ACCESS_TOKEN, ACCESS_SECRET)
        # api = tweepy.API(auth)
        
        # For demonstration, we'll use mock data
        mock_tweets = [
            "Loving the new update! So excited! 😊",
            "This service is terrible. Very disappointed.",
            "Amazing news today! Can't wait to see what happens next!",
            "I'm so angry about this situation. It's unacceptable!",
            "What a beautiful day! Perfect weather for outdoor activities."
        ]
        
        for tweet in mock_tweets[:count]:
            analysis = self.analyzer.analyze_comprehensive(tweet)
            self.results.append({
                'text': tweet,
                'emotion': analysis['dominant_emotion'],
                'timestamp': datetime.now(),
                'scores': analysis['emotion_scores']
            })
        
        return self.results
    
    def generate_report(self):
        """Generate a summary report of analyzed content"""
        df = pd.DataFrame(self.results)
        
        if not df.empty:
            emotion_counts = df['emotion'].value_counts()
            
            plt.figure(figsize=(10, 6))
            emotion_counts.plot(kind='bar')
            plt.title('Emotion Distribution in Social Media Posts')
            plt.xlabel('Emotions')
            plt.ylabel('Count')
            plt.xticks(rotation=45)
            plt.tight_layout()
            plt.show()
            
            return {
                'total_posts': len(df),
                'emotion_distribution': emotion_counts.to_dict(),
                'most_common_emotion': emotion_counts.idxmax()
            }
        
        return {}

# Example usage
monitor = SocialMediaEmotionMonitor(advanced_analyzer)
results = monitor.analyze_tweets("technology", count=5)
report = monitor.generate_report()

print("Social Media Emotion Report:")
print(report)
