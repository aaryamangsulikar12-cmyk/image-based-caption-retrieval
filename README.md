# 📸 SmartCaptioner — Image-Based Caption Retrieval

**SmartCaptioner** is an AI-powered multi-modal image caption retrieval system designed to automate context-aware, creative social media captioning. By replacing traditional CNN-LSTM generative models with **OpenAI's CLIP (Contrastive Language-Image Pretraining)** model (`openai/clip-vit-base-patch16`), SmartCaptioner maps image and textual data into a shared multi-modal embedding space to evaluate visual semantics and accurately retrieve contextually aligned captions.

## 🌟 Key Features

* **Multi-Modal Joint Alignment:** Uses OpenAI's CLIP model (`ViT-B/16`) to process images and text concurrently without relying on traditional sequential tokenization/LSTM loops.

* **Context-Aware Classification:** Classifies images across **16 curated categories** (e.g., *Mountain, Beach, Cats, Dogs, Monsoon, Cafe, Diwali, Christmas, Birthday, Baddie, Friends, Mirror, Sky, Couples, Sunkissed, Desi*).

* **Top-K Caption Retrieval:** Computes cosine similarity across pre-encoded candidate embeddings to return the top 5 most relevant captions instantly.

* **Interactive Caption Regeneration:** Includes a dynamic endpoint to cycle through alternative candidate caption batches for enhanced user personalization.

* **Cross-Platform Accessibility:** Features a responsive **Django REST API** backend powering both a web application and an Android mobile application built via **Kodular**.

## 📁 Dataset Details

* **Total Images:** 1,600 high-quality images sourced across 16 categories (100 images per category).

* **Total Captions:** 8,000 captions (5 human-curated captions per image).

* **Data Source:** Curated and categorized from Pinterest for relevant, modern social media trends.

## 🏗️ System Architecture & Workflow

```
┌─────────────────┐     ┌──────────────────┐     ┌───────────────────────┐
│  Image Input    │ ──> │ Image Preprocess │ ──> │ OpenAI CLIP Encoder   │
│  (Web / Mobile) │     │  (224x224, Normal)│     │ (Vision Transformer)  │
└─────────────────┘     └──────────────────┘     └──────────┬────────────┘
                                                            │
                                                     Image Embedding
                                                            │
                                                            ▼
┌─────────────────┐     ┌──────────────────┐     ┌───────────────────────┐
│ Top 5 Captions  │ <── │ Similarity Rank  │ <── │ Cosine Similarity     │
│ Output + Refresh│     │   (Top-K Search) │     │ (Image vs Text Space) │
└─────────────────┘     └──────────────────┘     └───────────────────────┘

```

1. **Preprocessing:** Input images are resized to $224 \times 224$ pixels and normalized for vision transformer input.

2. **Feature Extraction:** CLIP extracts a dense numerical embedding vector representing the core visual semantics of the image.

3. **Similarity Scoring & Retrieval:** Cosine similarity is computed against stored target text/category embeddings to isolate the optimal semantic match.

4. **API Output:** The backend delivers the top 5 ranked captions with an average latency under 3 seconds.

## 🛠️ Tech Stack & Tools

* **Core Language:** Python 3.x

* **Deep Learning / AI:** PyTorch, Hugging Face `transformers`, OpenCV, Torchvision, PIL, NumPy

* **Pre-trained Model:** OpenAI CLIP (`openai/clip-vit-base-patch16`)

* **Backend Framework:** Django, Django REST Framework (DRF)

* **Database:** SQLite

* **Mobile Frontend:** Kodular (REST API Integration)

* **Web Frontend:** HTML5, CSS3, JavaScript

## 📊 Results & Performance

* **Inference Time:** $< 3.0$ seconds average response time for upload-to-caption output.

* **Accuracy:** High contextual and semantic alignment verified across 16 diverse categories.

* **Overfitting Risk:** Eliminated by relying on zero-shot semantic matching via CLIP's pre-trained shared feature space instead of training fragile decoders from scratch.

## 🔮 Future Roadmap

* \[ \] **Multilingual Support:** Regional and global language translation (Hindi, Spanish, French).

* \[ \] **Hashtag Recommendation Engine:** Auto-generating trending hashtags (e.g., `#SunsetVibes`, `#FoodieLife`).

* \[ \] **Hybrid Generative Capabilities:** Integrating BLIP / GPT-4V for novel, completely un-retrieved generative captions.

* \[ \] **User Feedback Loop:** Dynamic fine-tuning based on user caption selections and regenerations.

## 🎓 Academic Credits

This project was carried out as part of the **Bachelor of Science in Data Science (B.Sc. DS)** dissertation at **Savitribai Phule Pune University (Department of Technology)** under the guidance of **Dr. Madhavi Chaudhari**.

**Project Members:**

* **Aarya Amar Mangsulikar** (BSC22DS01)

* **Dipti Dattatraya Dhavalikar** (BSC22DS31)

* **Gunjan Rakesh Agarwal** (BSC22DS40)
