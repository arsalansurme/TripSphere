# TripSphere 🌍
### Intelligent Travel Planning Desktop Application

**Plan smarter, discover more, and manage your entire journey in one place.**

TripSphere is an AI-assisted travel planning desktop application built with Python and PySide6/Qt6. It brings destination discovery, interactive maps, route planning, trip management, expense tracking, and voice-enabled AI assistance together in a unified desktop experience.

Designed to simplify travel planning, TripSphere combines mapping technologies, external travel services, local data storage, and Google's Gemini AI to help users explore destinations, organize journeys, and manage travel information through an intuitive graphical interface.

---

## 📌 Overview

Planning a trip often means switching between multiple applications to search destinations, explore attractions, calculate routes, organize itineraries, and track expenses.

TripSphere brings these activities together in one application. Users can discover places, visualize locations on an interactive map, create and manage trips, monitor their spending, save favorite destinations, maintain travel journals, and interact with an AI-powered travel assistant.

The application follows a modular architecture that separates the user interface, business logic, database access, external API integrations, and embedded web components.

### What makes TripSphere stand out?

- **AI-assisted travel planning:** Interact with a Gemini-powered assistant using natural-language requests and predefined application tools.
- **Interactive geographic exploration:** Search destinations, explore nearby points of interest, and visualize locations and routes.
- **Unified trip management:** Organize trips, stops, itinerary-related information, and travel expenses.
- **Budget awareness:** Record expenses and review spending through analytics and visualizations.
- **Voice interaction:** Communicate with the assistant using speech recognition and text-to-speech.
- **Local data persistence:** Store travel information in a SQLite database.
- **Integrated desktop experience:** Access the major features through a PySide6-based graphical interface.

---

## ✨ Features

### 🗺️ Destination Discovery and Interactive Maps

Explore destinations and view geographic information directly inside TripSphere.

- Search for locations and resolve them to geographic coordinates.
- Explore nearby attractions and points of interest.
- View location markers and route information on an interactive map.
- Pan and zoom around the map.
- Display map information through an embedded Leaflet interface.
- Use geocoding and place-discovery services to retrieve geographic information.

The map is rendered using Leaflet.js within Qt WebEngine, allowing Python application logic to communicate with the JavaScript-based map.

### 🧭 Route Planning

Plan journeys between locations and view useful route information.

- Resolve origin and destination locations.
- Calculate routes through the routing service.
- Retrieve distance, duration, and route geometry where available.
- Display route information on the interactive map.
- Support configured travel-mode options.
- Use fallback distance logic when supported by the routing implementation.

TripSphere uses the Open Source Routing Machine (OSRM) for route calculations.

### 🧳 Trip and Itinerary Management

Organize travel information in one place.

- Create and manage trips.
- Store origin and destination details.
- Maintain travel dates, traveler counts, and budget information.
- Manage trip stops.
- Associate expenses and itinerary-related data with trips.
- View trip details and route summaries.
- Complete or remove journeys through the available trip interface.

Trip data is persisted locally using SQLite, allowing stored information to remain available across application sessions.

### 💰 Expense Tracking and Budget Analytics

Keep travel spending organized throughout the planning process.

- Record travel expenses.
- Organize expenses by category.
- Associate expenses with trips.
- Review expense summaries.
- Compare spending against trip budgets.
- Visualize expense distributions and trends using charts.

Matplotlib is used for supported budget and expense visualizations.

### 🤖 AI Travel Assistant

TripSphere integrates Google's Gemini AI through the `google-genai` Python library.

The assistant provides a natural-language interface to travel-related capabilities. Rather than requiring users to issue only predefined text commands, the model can interpret a request and select an appropriate predefined application tool.

Supported tool categories include:

- Location search
- Route calculation
- Nearby-place discovery
- Hotel, flight, train, and bus search
- Activity discovery
- Trip creation and updates
- Expense creation
- Map location and route actions

The application exposes **13 predefined AI tools** through a controlled tool-calling mechanism. The application validates and executes supported tools rather than giving the model unrestricted Python execution access.

### 🎙️ Voice Interaction

TripSphere includes a voice-based interaction mode for communicating with the AI assistant.

The current voice pipeline uses:

1. SpeechRecognition to capture and transcribe user speech.
2. Gemini to interpret the request and generate a response.
3. Edge TTS to synthesize spoken output.
4. Windows audio playback mechanisms to play the generated speech.

The implementation includes conversational listening, assistant state handling, sentence-level speech generation, and fallback voice components.

The current voice playback implementation is Windows-oriented.

### 📔 Travel Journal

Maintain personal travel-related records through the journal interface.

- Create journal entries.
- Organize travel memories.
- Record mood information where supported.
- Associate optional photo paths with entries.

### ❤️ Favorites

Save places of interest for later access and simplify destination discovery.

### 🎲 Random Destination Discovery

Explore destination suggestions when you are looking for travel inspiration rather than planning around a specific location.

### ⚙️ Settings and Preferences

Configure available application preferences, including profile-related information, currency, and travel-mode settings.

### 💾 Local Data Persistence

TripSphere uses SQLite for local application data.

Its database layer supports structured storage for users, destinations, places, trips, stops, itinerary items, expenses, journal entries, favorites, and cached information.

The application also includes database initialization and migration logic to support changes to its schema.

---

## 🛠️ Technology Stack

| Technology | Purpose |
|---|---|
| Python | Core application logic and service integration |
| PySide6 / Qt6 | Desktop graphical user interface |
| Qt Signals and Slots | Event-driven communication |
| QThread | Background execution for supported application tasks |
| Qt WebEngine | Embedding web-based visual components |
| QWebChannel | Python–JavaScript communication |
| SQLite | Local relational data storage |
| Leaflet.js | Interactive map rendering |
| HTML / JavaScript | Embedded map and visual interfaces |
| Requests | HTTP communication with external services |
| Nominatim | Geocoding and reverse geocoding |
| Overpass API | OpenStreetMap point-of-interest discovery |
| OSRM | Route calculation |
| Google Gemini API | AI responses and function calling |
| SpeechRecognition | Speech-to-text |
| Edge TTS | Text-to-speech |
| Matplotlib | Budget and expense charts |
| python-dotenv | Environment-based configuration |

---

## 🏗️ Application Architecture

TripSphere uses a modular, layered desktop architecture.

### 1. Presentation Layer

Responsible for screens, widgets, forms, navigation, user interaction, and visual state.

Built with PySide6 and Qt6.

### 2. Service Layer

Contains application operations and business logic, including trip management, expense operations, recommendations, AI orchestration, and voice processing.

### 3. Data-Access Layer

Repositories encapsulate SQLite operations and provide a structured interface for storing and retrieving application data.

### 4. API Integration Layer

External-service modules handle geocoding, nearby places, routing, and AI requests.

### 5. Map and Embedded Web Layer

A Qt WebEngine view hosts HTML and JavaScript. Leaflet manages map rendering while a communication bridge allows Python and JavaScript to exchange data and actions.

### High-Level Architecture

```text
                    TRIPSPHERE
                         |
                         v
                    MainWindow
                         |
              +----------+----------+
              |                     |
              v                     v
          Navigation           Application Pages
                                    |
                                    v
                                Services
                                    |
                   +----------------+----------------+
                   |                |                |
                   v                v                v
               Repositories      Travel APIs       Gemini AI
                   |                |                |
                   v                v                v
                SQLite          External Data     AI Tools
                                    |
                                    v
                             Map / UI Updates
```

The AI assistant communicates with application capabilities through predefined tools, while the service and repository layers handle the corresponding operations.

---

## 🌐 External Services

TripSphere integrates with external services for selected travel and AI features.

| Service | Integration |
|---|---|
| Nominatim | Location search and reverse geocoding |
| Overpass API | Nearby points of interest |
| OSRM | Routing and route geometry |
| Google Gemini | Natural-language responses and tool calling |
| Google Speech Recognition | Speech transcription through SpeechRecognition |
| Edge TTS | Spoken response generation |
| OpenStreetMap-compatible map tiles | Geographic map display |

Availability and responsiveness of external services depend on network connectivity, service limits, and API behavior.

**Travel-provider note:** The current implementation includes portal links and template-based results for some travel-provider searches. Full live flight, hotel, or transport booking integration should not be assumed unless separately implemented and verified.

---

## 🚀 Getting Started

### Prerequisites

- Python version compatible with the project's dependencies.
- A compatible desktop environment.
- Windows for the current complete voice-playback path.
- Internet access for external maps, travel services, speech recognition, and Gemini.
- A Google Gemini API key for AI features.

## 🔐 Security and Configuration

TripSphere uses environment variables for API configuration and includes a controlled allowlist for AI tool execution.

Recommended repository practices:

- Keep `.env` out of version control.
- Commit `.env.example` without real secret values.
- Never publish API keys, private credentials, or personal database contents.
- Review external API dependencies and their terms of use.
- Keep dependencies updated and test changes before deployment.

Local persistence does not imply cloud synchronization or server-side backup.

---

## 🧪 Testing and Diagnostics

The repository includes tests for several application areas, including:

- AI assistant behavior
- Chat interface
- Gemini connectivity
- Gemini tool calling
- Nearby-place discovery
- Places-service resilience
- Voice service behavior

It also contains Windows and Qt WebEngine diagnostic utilities for investigating application-window and embedded-browser behavior.

Run tests according to the test files and environment configuration present in the repository. Tests that depend on network services or API credentials may require additional setup.

---

## 📁 Project Structure

The main application is organized into the following areas:

```text
travel_app/
├── main.py
├── app/
│   ├── config.py
│   ├── session.py
│   ├── api/
│   │   ├── geocoding.py
│   │   ├── places.py
│   │   └── routing.py
│   ├── database/
│   │   ├── db.py
│   │   ├── models.py
│   │   ├── repositories.py
│   │   └── seed_data.py
│   ├── map/
│   │   └── map_view.py
│   ├── services/
│   │   ├── assistant_agent.py
│   │   ├── gemini_client.py
│   │   ├── voice_service.py
│   │   ├── trip_service.py
│   │   ├── expense_service.py
│   │   ├── journal_service.py
│   │   ├── recommendation_service.py
│   │   └── travel_providers.py
│   └── ui/
│       ├── main_window.py
│       ├── startup.py
│       ├── dashboard.py
│       ├── explore.py
│       ├── trips.py
│       ├── trip_detail.py
│       ├── expenses.py
│       ├── budget.py
│       ├── journal.py
│       ├── favorites.py
│       ├── random_dest.py
│       ├── settings.py
│       ├── chat.py
│       └── widgets/
├── data/
├── logs/
├── tests/
├── requirements.txt
├── .env.example
└── README.md
```

This is a high-level view of the main source structure. Refer to the repository itself for the complete file inventory, runtime assets, database files, and diagnostic utilities.

---

## ⚠️ Current Limitations

- Several features rely on third-party services and therefore require internet access.
- Offline functionality is partial; external map tiles and API-backed searches may be unavailable offline.
- The voice implementation includes Windows-specific audio playback components.
- Some travel-provider results are template-based or use external portal links instead of full live booking APIs.
- API response times, availability, and usage limits are controlled partly by external providers.

These limitations should be considered when installing, demonstrating, or extending the application.

---

## 🔮 Potential Areas for Future Improvement

Possible future improvements include:

- Broader automated test coverage.
- More detailed performance monitoring and latency optimization.
- Expanded travel-provider API integrations.
- Improved offline access to cached geographic information.
- Cross-platform voice playback.
- Additional itinerary visualization and travel analytics.
- Further refinement of AI tool validation and error recovery.

These are potential enhancement areas, not claims that the features are already implemented.

---

## 🎯 Project Objective

TripSphere aims to make travel planning more organized and accessible by combining interactive geographic exploration, trip and expense management, and AI-assisted natural-language interaction in one desktop application.

It also serves as a practical demonstration of integrating Python desktop development, relational data storage, external APIs, embedded JavaScript mapping, background workers, and AI function calling into a single software system.

## 👨‍💻 Author

**Arsalan Surme**  
Developer of TripSphere

Linkedin Arsalansurme 
mail:arsalasnsurme@gmail.com.

---

**TripSphere — Explore destinations. Plan journeys. Manage travel smarter.**
