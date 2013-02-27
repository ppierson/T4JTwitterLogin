T4JTwitterLogin
===============

A simple android library for logging into twitter and posting tweets using the Twitter4J library. 
It is a quick and simple implementation, any suggestions or contributions are welcome :).


Logging into Twitter:
=======
First the login activity needs to be registered in your manifest:
```
  <activity
      android:name="com.ppierson.t4jtwitterlogin.T4JTwitterLoginActivity">
      <intent-filter>
          <action android:name="android.intent.action.VIEW" />
          <category android:name="android.intent.category.DEFAULT" />
          <category android:name="android.intent.category.BROWSABLE" />
          <data android:scheme="x-oauthflow-twitter" android:host="twitterlogin"/>
      </intent-filter>
  </activity>
```

Next you will need to override the onActivityResult method of whatever activity you will be initiating the twitter login from.
```
  private static final int TWITTER_LOGIN_REQUEST_CODE = 1;

  @Override
  public void onActivityResult(int requestCode, int resultCode, Intent data) {
  	super.onActivityResult(requestCode, resultCode, data);
  	Log.d("TAG", "ON ACTIVITY RESULT!");
  	if(requestCode == TWITTER_LOGIN_REQUEST_CODE){
  		Log.d("TAG", "TWITTER LOGIN REQUEST CODE");
  		if(resultCode == T4JTwitterLoginActivity.TWITTER_LOGIN_RESULT_CODE_SUCCESS){
  			Log.d("TAG", "TWITTER LOGIN SUCCESS");
  		}else if(resultCode == T4JTwitterLoginActivity.TWITTER_LOGIN_RESULT_CODE_FAILURE){
  			Log.d("TAG", "TWITTER LOGIN FAIL");
  		}else{
        //
  		}
  	}
  }
```

To initiate Twitter Login Activity:
```
  if (!T4JTwitterLoginActivity.isConnected(getActivity())){
  	Intent twitterLoginIntent = new Intent(getActivity(), T4JTwitterLoginActivity.class);
  	twitterLoginIntent.putExtra(T4JTwitterLoginActivity.TWITTER_CONSUMER_KEY, "YOUR CONSUMER KEY");
  	twitterLoginIntent.putExtra(T4JTwitterLoginActivity.TWITTER_CONSUMER_SECRET, "YOUR CONSUMER SECRET");
  	startActivityForResult(twitterLoginIntent, TWITTER_LOGIN_REQUEST_CODE);
  }
```

Posting a tweet:
=======

```
T4JTwitterFunctions.postToTwitter(getActivity().getApplicationContext(), getActivity(), TWITTER_CONSUMER_KEY, TWITTER_CONSUMER_SECRET, tweetString, new T4JTwitterFunctions.TwitterPostResponse() {
    @Override
    public void OnResult(Boolean success) {
    	// TODO Auto-generated method stub
    	if(success){
    		Toast.makeText(getActivity().getApplicationContext(), "Tweet posted successfully", Toast.LENGTH_SHORT).show();
    	}else{
    		Toast.makeText(getActivity().getApplicationContext(), "Tweet did not post!", Toast.LENGTH_SHORT).show();
    	}
    }
});

```

TODO:
=======
Add additional twitter functionality
Error handling, informative error responses

License
=======
```
//
//  Copyright (c) 2012 Patrick Pierson
//  
//  Permission is hereby granted, free of charge, to any person obtaining a copy
//  of this software and associated documentation files (the "Software"),
//  to deal in the Software without restriction, including without limitation the
//  rights to use, copy, modify, merge, publish, distribute, sublicense, and/or
//  sell copies of the Software, and to permit persons to whom the Software is
//  furnished to do so, subject to the following conditions:
//  
//  The above copyright notice and this permission notice shall be included in all
//  copies or substantial portions of the Software.
//  
//  THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED,
//  INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A
//  PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT
//  HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
//  OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
//  SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
//

```
