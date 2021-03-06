# DROELOE - Sunburn (Reimagined Presave)

![DROELOE - Sunburn (Reimagined) teaser](https://user-images.githubusercontent.com/10178648/123152129-88b03700-d464-11eb-8b61-7fc64cf87faa.gif)

This is an adapted showcase version of an application developed by me, Niels Kersic, for the record label [bitbird](https://bitbirdofficial.com/) and artist [DROELOE](https://www.instagram.com/droeloemusic/).
The purpose of this application was for people to presave DROELOE's new track 'Sunburn (Reimagined)', one of the singles of their (then) upcoming Anthology Album '[A Matter of Perspective](https://bitbird.lnk.to/amatterofperspective)'.

---
## The premise
As the name suggests, 'Sunburn (Reimagined)', is a reimagination of DROELOE's track Sunburn. Based on the lyrics, the theming for both tracks is based around trains and train stations. For this reason, we decided to center the presave campaign around a classic Dutch ticketing machine. People would be able to imagine their own journey and generate a ticket. This ticket could be downloaded after completing the presave to share on social media.

![Dutch National Rail ticketing machine](https://storage.googleapis.com/nielskersic/static-images/github/sunburn-presave-cover.jpg)

## How it's made
### Frontend
The frontend is an Angular 9 app that consists of two routes. The main route is where users can create their journey by filling in some text inputs and select a presave option (Spotify or Apple Music). The second route is where people land after completing the save. This is where they can download their generated train tickets and share them to social media. While some animations were considered, we chose to not implement them to stay closer to the ticketing machines from which we drew inspiration. The frontend also use of Apple's MusicKitJS, as this is required to enable login with Apple Music. Spotify auth follows the Oauth 2.0 Authorization Code Grant Flow (RFC-6749).

### Backend
The backend is a NodeJS Express application. This is where most of the interactions with the Spotify Web API and Apple Music API take place. The backend is also where tickets are generated using the [canvas package](https://www.npmjs.com/package/canvas). The canvas consists of a static background image onto which the user's text is added. The canvas is then written to a JPG file to be stored on Google Cloud Storage for retrieval by the user.

### Infrastructure
- Frontend is hosted using Firebase Hosting
- Data is stored in Firestore (only in the original version)
- API is deployed on Google Cloud Run (to keep costs low and to scale with demand) 

## What's different in this version
- The original application would store Spotify and Apple Music tokens in Firestore. On release day, these tokens were used to save the track to the user's libraries. No data is stored in Firestore for the showcase version. The track is instantly saved to the user's library instead.
- To keep accurate metrics of presaves, Firestore Cloud Functions would fire on each new document add or remove.
- The original implemented both Google Analytics and Facebook Pixel to track events for marketing purposes. These were removed for the showcase version.
- In the original ticket generator, the code at the bottom would auto-increment with each presave. Since presaves are not stored and such a counter is not kept, a random number is generated instead. 

## What could be improved
- TESTS! The original application was developed under a very tight deadline, so no tests were written.
- Cleaner code. This presave app was adapted from an earlier presave campaign. This saved a lot of time implementing elements like the Spotify and Apple Music login, but it also lead to some unused code remaining in the app.
- Moving the Spotify OAuth flow to a pop-up. This would prevent having to pass around the unique ID for each presave (used for the user-generated tickets) in the URL.
- Small UI improvements and bug fixes.

---

# Generated ticket examples
![Horizontal ticket example](https://storage.googleapis.com/nielskersic/static-images/github/sunburn-example-ticket-horizontal.jpg)
![Vertical ticket example](https://storage.googleapis.com/nielskersic/static-images/github/sunburn-example-ticket-vertical.jpg)
