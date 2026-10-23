# TravelScout

TravelScout is a travel-planning website frontend built with **React, TypeScript, and Vite**. It provides a landing page and separate sections for browsing flights and hotels, viewing individual listing details, creating an account, signing in, and managing a user profile.

The repository contains the frontend application. Authentication and profile operations are configured to call a separate API at `http://localhost:4000/api/v1`, while flight and hotel search pages import local JSON data.

## Features

- **Travel homepage:** Landing page with navigation, a travel-themed hero section, a “Next Trip” section, customer testimonials, and footer.
- **Flight listings:** Browse flight data from the local `src/mockJSONFiles/flights.json` file.
- **Flight details:** Open a flight-specific page using its ID.
- **Hotel listings:** Browse hotel data from the local `src/mockJSONFiles/hotels.json` file.
- **Hotel details:** Open a hotel-specific page using its ID.
- **User registration:** Sign-up form for name, email, password confirmation, and phone number.
- **User login and logout:** Authentication requests are sent to the configured backend API.
- **Profile page:** User profile area with profile-update support.
- **Route handling:** Client-side routing for the homepage, authentication pages, profile, flight and hotel pages, About Us, access-denied, and not-found pages.
- **Responsive navigation styling:** Uses Tailwind CSS utility classes for layouts and mobile navigation.
- **Notifications:** Uses `react-hot-toast` for success and error messages in authentication flows.

> **Important:** The repository is the frontend only. The API server is not included in this ZIP. Flight and hotel pages use local JSON data, so the project should not be described as a live flight-booking or hotel-booking service unless a real booking backend has been added separately.

## Tech Stack

| Area | Technology |
|---|---|
| Frontend framework | React 18 |
| Language | TypeScript |
| Development server and bundler | Vite 5 |
| Routing | React Router DOM 6 |
| State management | Redux Toolkit and React Redux |
| HTTP requests | Axios |
| Styling | Tailwind CSS, DaisyUI |
| Icons | Lucide React, React Icons |
| Notifications | React Hot Toast |
| Charts | Chart.js, React Chart.js 2 |
| Internationalization dependency | react-i18next |
| Cookie utility | js-cookie |

## Project Structure

```text
travel-repo-main/
├── index.html
├── package.json
├── vite.config.ts
├── tailwind.config.js
├── postcss.config.js
├── tsconfig.json
└── src/
    ├── App.tsx                    # Application routes
    ├── main.tsx                   # React entry point
    ├── index.css                  # Global styles
    ├── Assets/
    │   ├── flights/               # Flight destination images
    │   └── hotels/                # Hotel images
    ├── Components/
    │   ├── FlightDetailsPage.tsx
    │   ├── FlightsSearchPage.tsx
    │   ├── Footer.tsx
    │   ├── HotelDetailsPage.tsx
    │   ├── HotelsSearchPage.tsx
    │   ├── NextTrip.tsx
    │   └── ProfilePage.tsx
    ├── Helpers/
    │   ├── Hooks.ts               # Typed Redux hooks
    │   ├── axiosInstance.ts        # API base URL and Axios config
    │   └── regexMatcher.ts
    ├── Pages/
    │   ├── Homepage.tsx
    │   ├── Login.tsx
    │   ├── Signup.tsx
    │   ├── Aboutus.tsx
    │   ├── Denied.tsx
    │   └── NotFound.tsx
    ├── Redux/
    │   ├── Slices/
    │   │   └── authSlice.reducer.ts
    │   └── store.ts
    └── mockJSONFiles/
        ├── flights.json
        └── hotels.json
```

## Getting Started

### Prerequisites

- Node.js (preferably a current LTS version)
- npm
- The separate backend API, if you want registration, login, logout, or profile operations to work

### 1. Clone the repository

```bash
git clone <repository-url>
cd travel-repo-main
```

Replace `<repository-url>` with the URL of your repository.

### 2. Install dependencies

```bash
npm install
```

### 3. Configure the backend URL

The Axios instance is configured in `src/Helpers/axiosInstance.ts` with this base URL:

```text
http://localhost:4000/api/v1
```

Make sure the backend is running at that address for API-backed account and profile operations. If your API uses a different address, update the base URL in that file.

The configured frontend requests include:

- `POST /user/register`
- `POST /user/login`
- `POST /user/logout`
- `PUT /user/update/:id`
- `GET /user/me`

These endpoints are expected by the frontend; their implementation is not included in this repository.

### 4. Start the development server

```bash
npm run dev
```

Vite will print the local development URL in the terminal, usually `http://localhost:5173`.

### 5. Build for production

```bash
npm run build
```

To preview the production build locally:

```bash
npm run preview
```

### 6. Run linting

```bash
npm run lint
```

The `package.json` also defines an `npm test` script, but the repository should have its Jest test configuration and dependencies verified before relying on that command.

## Application Routes

| Route | Page |
|---|---|
| `/` | Homepage |
| `/signup` | Create account |
| `/login` | Login |
| `/profile` | User profile |
| `/flights` | Flight listings |
| `/flights/:flightId` | Flight details |
| `/hotels` | Hotel listings |
| `/hotels/:hotelId` | Hotel details |
| `/aboutus` | About Us |
| `/denied` | Access-denied page |
| Any unmatched route | Not-found page |

## Data and State Management

### Flight and hotel data

The flight and hotel search components import local JSON files:

- `src/mockJSONFiles/flights.json`
- `src/mockJSONFiles/hotels.json`

This allows the frontend to render sample listing data without a live travel inventory API. The listing details are selected through route parameters.

### Authentication state

Redux Toolkit manages authentication state in `src/Redux/Slices/authSlice.reducer.ts`. The slice defines asynchronous actions for registration, login, logout, fetching the current user, and updating a profile. The current implementation also stores user data and a login flag in `localStorage`.

The Axios instance sets `withCredentials: true`, so the backend must be configured appropriately for cross-origin requests and cookie-based credentials if that is how its authentication works.

## Current Limitations

- The backend API is referenced by the frontend but is not included in this repository.
- Flight and hotel inventory comes from local JSON files, not a live airline or hotel provider.
- The presence of flight and hotel details pages does not by itself mean real bookings, payments, or ticket issuance are supported.
- The frontend code contains a note about authentication tokens/cookies not being set correctly when using a hosted backend. Authentication should be tested with the actual backend before deployment.
- The project stores an authentication flag and user data in `localStorage`; this client-side state alone should not be treated as proof of authorization. Protected operations must be enforced by the backend.
- Production deployment requires updating the API URL and configuring CORS, credentials, and secure authentication appropriately.

## Possible Improvements

- Move the API base URL into a Vite environment variable, such as `VITE_API_BASE_URL`.
- Add automated tests for forms, route behavior, and Redux authentication flows.
- Add loading, empty, and error states for flight and hotel listings.
- Improve form validation and accessible labels.
- Connect flight and hotel listings to a verified live inventory API if real-time search is required.
- Implement booking, payment, and confirmation flows only with a secure backend and a suitable provider.
- Add deployment instructions for the frontend and backend separately.

## Contributor

- Name: anushkaagr3001
- GitHub: https://github.com/anushkaagr3001

- Role: Project contributor and maintainer

## Disclaimer

TravelScout is a travel-planning frontend project. Listing data is local sample data, and the project is not presented as an airline, hotel chain, or booking provider. Confirm prices, availability, and booking details through official providers.

## License

No license information was identified in the supplied project files. Add a `LICENSE` file if you intend to specify how others may use, modify, or distribute the project.
"# travel-repo" 
