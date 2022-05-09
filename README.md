# Example Token Refresh Server

An node server capable of swapping and refreshing tokens provided by Spotify API.

I took this straight from [here](https://github.com/cjam/react-native-spotify-remote/tree/7f688a211080ee5d4cd302df3a478e40441c3cad/example-server)

Deployed on Heroku. Some pages that might benefit you:
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
Can also specify `PORT` if you want to run it on something other than 3000 (or, if you're using Heroku like me, the default Heroku port).
> Optionally this can be done on the command line as well when starting up the server via node

3. Run server using: `npm run start`
4. In you the *Spotify for Bike* app set `tokenSwapURL` to `http://<SERVER_URL>:<PORT>/swap` and `tokenRefreshURL` to `http://<SERVER_URL>:<PORT>/refresh`, replacing `<SERVER_URL>` and `<PORT>` with your server URL and port.
