# Sentiment_Analysis-Awesome
🎭 Sentiment Analysis Awesome
Show Image
Show Image
Show Image
Show Image
A powerful, interactive sentiment analysis tool leveraging Google's Gemini 1.5 Flash model to classify text sentiment with confidence scoring.
📋 License Notice
This software is licensed under a Custom Non-Commercial License.

✅ Free for individuals for personal, educational, and non-monetized use
⚠️ Commercial entities (companies, enterprises, for-profit organizations) must obtain written permission and agree to revenue sharing
📧 See LICENSE for full details or contact for commercial licensing

🔑 Getting Your Google Gemini API Key (REQUIRED)
This tool requires a Google Gemini API key. Follow these detailed steps:
Step 1: Access Google AI Studio

Navigate to Google AI Studio
Sign in with your Google account
You'll be redirected to the Google AI Studio dashboard

Step 2: Create Your API Key

Click on "Get API Key" in the left sidebar
You'll see a page titled "API keys"
Click the "Create API Key" button
Choose an existing Google Cloud project or create a new one:

For new users: Select "Create API key in new project"
For existing GCP users: Select your project from the dropdown



Step 3: Copy and Secure Your Key

Your API key will be generated and displayed
IMPORTANT: Copy this key immediately and store it securely
This key will look something like: AIzaSyD-XXXXXXXXXX_XXXXXXXXXXXXX
Never commit this key to version control!

Step 4: Understand the Limits

Free Tier includes:

15 RPM (requests per minute)
1 million TPM (tokens per minute)
1,500 RPD (requests per day)


Perfect for personal projects and development
Check current limits

Step 5: Set Up Your API Key
For Google Colab (Easiest):

In your Colab notebook, click the 🔑 key icon in the left sidebar
Click "Add new secret"
Name it: GOOGLE_API_KEY
Paste your API key as the value
Click "Save"
The key is now securely stored and accessible to your notebook

For Local Development:
Option A: Environment Variable (Recommended)
bash# On macOS/Linux:
echo 'export GOOGLE_API_KEY="your-api-key-here"' >> ~/.bashrc
source ~/.bashrc

# On Windows (Command Prompt):
setx GOOGLE_API_KEY "your-api-key-here"

# On Windows (PowerShell):
[Environment]::SetEnvironmentVariable("GOOGLE_API_KEY", "your-api-key-here", "User")
Option B: .env File (Development Only)

Create a .env file in your project root:

envGOOGLE_API_KEY=your-api-key-here

Add .env to your .gitignore file (CRITICAL!)
Use python-dotenv to load it:

pythonfrom dotenv import load_dotenv
load_dotenv()
Option C: Config File (Alternative)

Create config.json:

json{
  "GOOGLE_API_KEY": "your-api-key-here"
}

Add config.json to .gitignore
Load in Python:

pythonimport json
with open('config.json') as f:
    config = json.load(f)
    GOOGLE_API_KEY = config['GOOGLE_API_KEY']
⚠️ Security Best Practices

NEVER hardcode your API key in your source code
NEVER commit your API key to GitHub
ALWAYS add API key files to .gitignore
USE environment variables or secure secret managers in production
ROTATE your keys regularly
MONITOR your usage in Google Cloud Console

✨ Features

🤖 AI-Powered Analysis: Utilizes Google's state-of-the-art Gemini 1.5 Flash model for accurate sentiment classification
📊 Confidence Scoring: Provides confidence levels (0-1) for each sentiment prediction
🎯 Three-Way Classification: Detects positive, negative, and neutral sentiments
🖥️ Interactive UI: User-friendly widget interface for easy text input and analysis
⚡ Real-time Processing: Instant sentiment analysis with clear results display
🔧 Function Calling: Leverages Gemini's function calling capabilities for structured outputs

🚀 Quick Start
Prerequisites

Python 3.7 or higher
Google account for API key
Google Colab account (for easiest setup) or Jupyter Notebook for local use

Installation

Clone the repository

bash   git clone https://github.com/yourusername/sentiment-analysis-awesome.git
   cd sentiment-analysis-awesome

Install dependencies

bash   pip install -r requirements.txt
   # Or manually:
   pip install google-generativeai ipywidgets python-dotenv

Set up your API key (See detailed instructions above)

📖 Usage
Running in Google Colab (Recommended for Beginners)

Open the notebook in Google Colab using the badge above
Add your API key to Colab's secrets manager (see API key section)
Run all cells
Enter your text in the text area
Click "Analyze Sentiment" to get results

Running Locally in Jupyter Notebook
bash# Start Jupyter Notebook
jupyter notebook

# Or Jupyter Lab
jupyter lab

# Open sentiment_analysis_awesome.ipynb
Using the Standalone Script
bash# Set your API key
export GOOGLE_API_KEY="your-api-key-here"

# Run the standalone version
python sentiment_analysis_standalone.py
Example Usage
python# The tool will analyze text like:
# Input: "I absolutely love this new feature! It's amazing!"
# Output: 
#   Sentiment: positive
#   Confidence: 0.95

# Input: "This is terrible and completely unusable."
# Output:
#   Sentiment: negative
#   Confidence: 0.92

# Input: "The weather is cloudy today."
# Output:
#   Sentiment: neutral
#   Confidence: 0.88
🛠️ How It Works

API Key Validation: Checks for valid Gemini API key
Model Initialization: Configures Gemini model with sentiment analysis function
User Input: Text entered through interactive widget interface
API Processing: Gemini model analyzes text using function calling
Result Extraction: Sentiment and confidence extracted from structured response
Display: Clear presentation of results with confidence scores

Architecture Flow
┌─────────────────┐
│   User Input    │
│   (Text Area)   │
└────────┬────────┘
         │
    ┌────▼────┐
    │ Validate │
    │ API Key  │
    └────┬────┘
         │
    ┌────▼────┐
    │ Analyze │
    │ Button  │
    └────┬────┘
         │
┌────────▼────────┐
│  Gemini 1.5     │
│  Flash Model    │
│  (Function Call)│
└────────┬────────┘
         │
┌────────▼────────┐
│ Parse Response  │
│ Extract Values  │
└────────┬────────┘
         │
┌────────▼────────┐
│  Display        │
│  • Sentiment    │
│  • Confidence   │
│  • Text Echo    │
└─────────────────┘
🔧 Configuration & Customization
Model Selection
python# Use different Gemini models based on your needs
gemini_model = genai.GenerativeModel(
    'gemini-1.5-pro-latest',     # Most capable, higher cost
    # 'gemini-1.5-flash-latest',  # Balanced performance (default)
    # 'gemini-1.0-pro',           # Legacy stable version
    tools=[sentiment_analysis_tool]
)
Adjust UI Components
python# Customize text input widget
text_input = widgets.Textarea(
    value='',
    placeholder='Enter text to analyze (max 1000 characters)',
    description='Text:',
    disabled=False,
    layout={'width': '600px', 'height': '150px'},
    style={'description_width': 'initial'}
)

# Add character counter
char_counter = widgets.HTML(value='0 / 1000 characters')
Enhanced Error Handling
pythondef analyze_text_enhanced(text):
    try:
        # Check API key
        if not GOOGLE_API_KEY:
            return {"error": "API key not configured"}
        
        # Validate input
        if len(text) > 1000:
            return {"error": "Text too long (max 1000 characters)"}
        
        # Add retry logic
        max_retries = 3
        for attempt in range(max_retries):
            try:
                response = gemini_model.generate_content(...)
                break
            except Exception as e:
                if attempt == max_retries - 1:
                    raise
                time.sleep(2 ** attempt)  # Exponential backoff
                
    except Exception as e:
        return {"error": f"Analysis failed: {str(e)}"}
🤝 Contributing
We welcome contributions! Please see our Contributing Guidelines.

Fork the repository
Create your feature branch (git checkout -b feature/AmazingFeature)
Commit changes (git commit -m 'Add some AmazingFeature')
Push to branch (git push origin feature/AmazingFeature)
Open a Pull Request

Development Setup
bash# Clone your fork
git clone https://github.com/yourusername/sentiment-analysis-awesome.git

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install in development mode
pip install -e .
pip install -r requirements-dev.txt

# Run tests
pytest tests/
📝 Roadmap
Version 1.1 (Next Release)

 Batch processing for multiple texts
 Export results to CSV/JSON
 Add language detection

Version 1.2

 Multi-language support (Spanish, French, German, etc.)
 Emotion detection (joy, anger, fear, surprise, etc.)
 Sentiment intensity levels (very positive, slightly negative, etc.)

Version 2.0

 REST API wrapper with FastAPI
 Web application with Streamlit
 Historical sentiment tracking
 Custom model fine-tuning options

🐛 Troubleshooting
Common Issues and Solutions
IssueSolution"API key not found"Ensure GOOGLE_API_KEY is properly set in environment or secrets"Quota exceeded"Check your API usage and limits"Module not found"Run pip install -r requirements.txt"Widget not displaying"Ensure you're in Jupyter/Colab environment with ipywidgets enabled"Connection error"Check internet connection and firewall settings"Invalid API key"Verify key in Google AI Studio
Getting Help

📖 Check the Wiki
🐛 Report bugs via GitHub Issues
💬 Join our Discord community
📧 Email support: your-email@example.com

📚 Resources

Google Gemini Documentation
Gemini API Reference
Function Calling Guide
Sentiment Analysis Best Practices
Google Cloud Pricing Calculator

📄 License
This project is licensed under a Custom Non-Commercial License:

Free for individuals for personal, educational, and non-monetized use
Commercial use requires written permission and revenue sharing agreement

See LICENSE file for complete details.
For commercial licensing inquiries: your-email@example.com
🙏 Acknowledgments

Google Gemini team for the powerful API
Google Colab for free computing environment
IPyWidgets team for interactive UI components
Open-source community for continuous inspiration

👤 Author
Your Name

GitHub: @yourusername
LinkedIn: Your Name
Twitter: @yourtwitter


<p align="center">
Made with ❤️ for the community<br>
Remember: Be kind, code responsibly, and share knowledge freely (when non-commercial)
</p>
Sentiment Analysis 
