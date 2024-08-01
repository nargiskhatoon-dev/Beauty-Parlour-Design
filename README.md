# Beauty-Parlour-Design
chore(deps): bump tmpl from 1.0.4 to 1.0.5 in /frontend
Bumps [tmpl](https://github.com/daaku/nodejs-tmpl) from 1.0.4 to 1.0.5.
- [Release notes](https://github.com/daaku/nodejs-tmpl/releases)
- [Commits](https://github.com/daaku/nodejs-tmpl/commits/v1.0.5)

---
updated-dependencies:
- dependency-name: tmpl
  dependency-type: indirect
...
@@ -19,7 +19,7 @@ export const loadUser = () => async (dispatch) => {
	const body = JSON.stringify({
		weekday: moment().isoWeekday(),
	})
	console.log(body)

	dispatch({ type: AUTH_LOADING })

	try {
@@ -32,7 +32,7 @@ export const loadUser = () => async (dispatch) => {
			type: AUTH_SUCCESS,
			payload: res.data,
		})
		dispatch(getOrCreateBusinessData(res.data.businesses[0].id))
		await dispatch(getOrCreateBusinessData(res.data.businesses[0].id))
	} catch (err) {
		dispatch({
			type: AUTH_ERROR,
@@ -62,7 +62,9 @@ export const login = (email, password, setErrors) => async (dispatch) => {

		if (res.data.user.businesses.length > 0) {
			NotificationManager.success(res.data.message, 'Zalogowano')
			dispatch(getOrCreateBusinessData(res.data.user.businesses[0].id))
			await dispatch(
				getOrCreateBusinessData(res.data.user.businesses[0].id)
			)
		}

		dispatch({ type: CLEAR_MEETINGS })
  6 changes: 2 additions & 4 deletions6  
frontend/src/redux/reducers/data.js
Original file line number	Diff line number	Diff line change
@@ -188,13 +188,11 @@ export default function (state = initialState, action) {
			request.onload = function () {
				context.decodeAudioData(
					request.response,
					function (response) {
					(response) => {
						source.buffer = response
						source.start(0) //play audio immediately
					},
					function () {
						console.error('The request failed.')
					}
					() => console.error('The request failed.')
				)
			}
			request.send()
