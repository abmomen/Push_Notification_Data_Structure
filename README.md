#### Push Notification Data Structure
##### Sending Notifications to a Number of Tokens.
##### To send notificaton to a topic Go Admin SDK uses User FCM token
```Go
  type MulticastMessage struct {
	Tokens       []string
	Data         map[string]string
	Notification *Notification
	Android      *AndroidConfig
	Webpush      *WebpushConfig
	APNS         *APNSConfig
}
```
#### Breakdown of MulticastMessage
##### Here Notification contains following datas:
```Go
// Notification is the basic notification template to use across all platforms.
type Notification struct {
	Title    string `json:"title,omitempty"`
	Body     string `json:"body,omitempty"`
	ImageURL string `json:"image,omitempty"`
}
```
##### Here Android contains following datas:
```Go
// AndroidConfig contains messaging options specific to the Android platform.
type AndroidConfig struct {
	CollapseKey           string               `json:"collapse_key,omitempty"`
	Priority              string               `json:"priority,omitempty"` // one of "normal" or "high"
	TTL                   *time.Duration       `json:"-"`
	RestrictedPackageName string               `json:"restricted_package_name,omitempty"`
	Data                  map[string]string    `json:"data,omitempty"` // if specified, overrides the Data field on Message type
	Notification          *AndroidNotification `json:"notification,omitempty"`
	FCMOptions            *AndroidFCMOptions   `json:"fcm_options,omitempty"`
}
```
##### Here Webpush contains following datas:
```Go
// WebpushConfig contains messaging options specific to the WebPush protocol.
//
// See https://tools.ietf.org/html/rfc8030#section-5 for additional details, and supported
// headers.
type WebpushConfig struct {
	Headers      map[string]string    `json:"headers,omitempty"`
	Data         map[string]string    `json:"data,omitempty"`
	Notification *WebpushNotification `json:"notification,omitempty"`
	FcmOptions   *WebpushFcmOptions   `json:"fcm_options,omitempty"`
}
```
##### Here APNS contains following datas:
```Go
// APNSConfig contains messaging options specific to the Apple Push Notification Service (APNS).
//
// See https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/CommunicatingwithAPNs.html
// for more details on supported headers and payload keys.
type APNSConfig struct {
	Headers    map[string]string `json:"headers,omitempty"`
	Payload    *APNSPayload      `json:"payload,omitempty"`
	FCMOptions *APNSFCMOptions   `json:"fcm_options,omitempty"`
}
```
#### Breakdown of AndroidConfig 
```Go
// AndroidNotification is a notification to send to Android devices.
type AndroidNotification struct {
	Title                 string                        `json:"title,omitempty"` // if specified, overrides the Title field of the Notification type
	Body                  string                        `json:"body,omitempty"`  // if specified, overrides the Body field of the Notification type
	Icon                  string                        `json:"icon,omitempty"`
	Color                 string                        `json:"color,omitempty"` // notification color in #RRGGBB format
	Sound                 string                        `json:"sound,omitempty"`
	Tag                   string                        `json:"tag,omitempty"`
	ClickAction           string                        `json:"click_action,omitempty"`
	BodyLocKey            string                        `json:"body_loc_key,omitempty"`
	BodyLocArgs           []string                      `json:"body_loc_args,omitempty"`
	TitleLocKey           string                        `json:"title_loc_key,omitempty"`
	TitleLocArgs          []string                      `json:"title_loc_args,omitempty"`
	ChannelID             string                        `json:"channel_id,omitempty"`
	ImageURL              string                        `json:"image,omitempty"`
	Ticker                string                        `json:"ticker,omitempty"`
	Sticky                bool                          `json:"sticky,omitempty"`
	EventTimestamp        *time.Time                    `json:"-"`
	LocalOnly             bool                          `json:"local_only,omitempty"`
	Priority              AndroidNotificationPriority   `json:"-"`
	VibrateTimingMillis   []int64                       `json:"-"`
	DefaultVibrateTimings bool                          `json:"default_vibrate_timings,omitempty"`
	DefaultSound          bool                          `json:"default_sound,omitempty"`
	LightSettings         *LightSettings                `json:"light_settings,omitempty"`
	DefaultLightSettings  bool                          `json:"default_light_settings,omitempty"`
	Visibility            AndroidNotificationVisibility `json:"-"`
	NotificationCount     *int                          `json:"notification_count,omitempty"`
}
```
```Go
// AndroidFCMOptions contains additional options for features provided by the FCM Android SDK.
type AndroidFCMOptions struct {
	AnalyticsLabel string `json:"analytics_label,omitempty"`
}
```

#### Breakdown of WebpushConfig
```Go
// WebpushNotification is a notification to send via WebPush protocol.
//
// See https://developer.mozilla.org/en-US/docs/Web/API/notification/Notification for additional
// details.
type WebpushNotification struct {
	Actions            []*WebpushNotificationAction `json:"actions,omitempty"`
	Title              string                       `json:"title,omitempty"` // if specified, overrides the Title field of the Notification type
	Body               string                       `json:"body,omitempty"`  // if specified, overrides the Body field of the Notification type
	Icon               string                       `json:"icon,omitempty"`
	Badge              string                       `json:"badge,omitempty"`
	Direction          string                       `json:"dir,omitempty"` // one of 'ltr' or 'rtl'
	Data               interface{}                  `json:"data,omitempty"`
	Image              string                       `json:"image,omitempty"`
	Language           string                       `json:"lang,omitempty"`
	Renotify           bool                         `json:"renotify,omitempty"`
	RequireInteraction bool                         `json:"requireInteraction,omitempty"`
	Silent             bool                         `json:"silent,omitempty"`
	Tag                string                       `json:"tag,omitempty"`
	TimestampMillis    *int64                       `json:"timestamp,omitempty"`
	Vibrate            []int                        `json:"vibrate,omitempty"`
	CustomData         map[string]interface{}
}

```
```Go
// WebpushFcmOptions contains additional options for features provided by the FCM web SDK.
type WebpushFcmOptions struct {
	Link string `json:"link,omitempty"`
}
```
#### Breakdown of APNSConfig
```Go
type APNSPayload struct {
	Aps        *Aps                   `json:"aps,omitempty"`
	CustomData map[string]interface{} `json:"-"`
}
```
```Go
type APNSFCMOptions struct {
	AnalyticsLabel string `json:"analytics_label,omitempty"`
	ImageURL       string `json:"image,omitempty"`
}
```
