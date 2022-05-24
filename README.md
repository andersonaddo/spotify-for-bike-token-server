# Example Token Refresh Server

An node server capable of swapping and refreshing tokens provided by Spotify API.

I took this straight from [here](https://github.com/cjam/react-native-spotify-remote/tree/7f688a211080ee5d4cd302df3a478e40441c3cad/example-server) to be used with [this app](https://github.com/andersonaddo/spotify-for-bike-app).

I deployed this on Heroku. Some pages that might benefit you:
- https://devcenter.heroku.com/articles/getting-started-with-nodejs
- https://devcenter.heroku.com/articles/deploying-nodejs

## Usage

1. Install dependencies using: 
```sh
npm install
```
2. Create a `.env` file in the root of this directory with the following entries acquired from [Spotify Developer Dashboard](https://developer.spotify.com/dashboard/applications) :
> ⚠️ Don't commit the `.env` file to your repo ⚠️

```env
SPOTIFY_CLIENT_ID="client_id_from_spotify_dashboard"
SPOTIFY_CLIENT_SECRET="client_secret_from_spotify_dashboard"
SPOTIFY_CLIENT_CALLBACK="callback_registered_in_spotify_dashboard"
ENCRYPTION_SECRET="THISWILLBEABIGSECRET"
ENCRYPTION_METHOD="aes-256-ctr"
```
Can also specify `PORT` if needed. This isn't needed if you're using Heroku.

3. Run server using: `npm run start`
4. In you the *Spotify for Bike* app set `tokenSwapURL` to `http://<SERVER_URL>:<PORT (if needed)>/swap` and `tokenRefreshURL` to `http://<SERVER_URL>:<PORT (if needed)>/refresh`, replacing `<SERVER_URL>` and `<PORT>` with your server URL and port (if needed).

## Why is this needed?

Spotify's [authentication flow](https://developer.spotify.com/documentation/general/guides/authorization/) is based on OAuth 2.0. Part of that [flow](https://developer.spotify.com/documentation/general/guides/authorization/code-flow/) makes use of a client secret (which is a secret to your Spotify App you can get on the Developer Dashboard) to [refresh auth tokens](https://developer.spotify.com/documentation/ios/guides/token-swap-and-refresh/). The problem is, this secret has to be provided by the person asking for the token refreshes, and secrets are never safe on clients. So, offloading that to a sever (and the client will just talk to an endpoint from that server when it wants it to get new tokens on it's behalf) is [safer](https://johnnycrazy.github.io/SpotifyAPI-NET/docs/token_swap/).

Learn more about secrets [here](https://security.stackexchange.com/questions/225397/what-is-the-purpose-of-the-oauth2-client-secret), and some new methods (that we don't use) to make them safer [here](https://dropbox.tech/developers/pkce--what-and-why-).
