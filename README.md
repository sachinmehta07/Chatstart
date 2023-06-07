# Chatstart


Set FirstActivity Text.


User
I want one simple Android application so there is three activity in first activity contains one single textview msg nd in third nd second activity we can set text so just want java code nd in that the first activity text should be set by the third activity set text so use startresultactivyforresult i know it's deprecated but use this only 

ChatGPT
Sure! I can help you with the Java code for your Android application that consists of three activities. Here's an example that demonstrates how to set the text of the first activity using the third activity's input text using startActivityForResult() (even though it's deprecated):

FirstActivity.java:

java
Copy code
import android.app.Activity;
import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.TextView;

public class FirstActivity extends Activity {
    private TextView textView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_first);
        textView = findViewById(R.id.textView);
    }

    public void goToSecondActivity(View view) {
        Intent intent = new Intent(this, SecondActivity.class);
        startActivityForResult(intent, 1);
    }

    public void setTextFromThirdActivity(String text) {
        textView.setText(text);
    }

    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);

        if (requestCode == 1 && resultCode == RESULT_OK) {
            String text = data.getStringExtra("text");
            setTextFromThirdActivity(text);
        }
    }
}
SecondActivity.java:

java
Copy code
import android.app.Activity;
import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.EditText;

public class SecondActivity extends Activity {
    private EditText editText;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_second);
        editText = findViewById(R.id.editText);
    }

    public void goToThirdActivity(View view) {
        String text = editText.getText().toString();
        Intent intent = new Intent(this, ThirdActivity.class);
        intent.putExtra("text", text);
        startActivityForResult(intent, 2);
    }
}
ThirdActivity.java:

java
Copy code
import android.app.Activity;
import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.EditText;

public class ThirdActivity extends Activity {
    private EditText editText;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_third);
        editText = findViewById(R.id.editText);
    }

    public void setTextAndFinish(View view) {
        String text = editText.getText().toString();
        Intent intent = new Intent();
        intent.putExtra("text", text);
        setResult(RESULT_OK, intent);
        finish();
    }
}
Make sure to create the corresponding layout XML files (activity_first.xml, activity_second.xml, activity_third.xml) for each activity and include the necessary views (TextView, EditText, etc.) as required.

Please note that using startActivityForResult() is deprecated since Android 11, and it's recommended to use ActivityResultContract and ActivityResultLauncher for achieving similar functionality in newer Android versions.





Send a message.


