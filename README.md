# MA

package com.example.calculator;
import androidx.appcompat.app.AppCompatActivity;
import android.annotation.SuppressLint;
import android.app.Activity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import android.os.Bundle;
public class MainActivity extends AppCompatActivity {
/** Called when the activity is first created. */
@Override
    public void onCreate(Bundle savedInstanceState) {
super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
EditText et1 =findViewById(R.id.editTextTextPersonName);
EditText et2 =findViewById(R.id.editTextTextPersonName2);
        Button add =findViewById(R.id.button);
        Button sub =findViewById(R.id.button3);
        Button mul =findViewById(R.id.button4);
        Button div =findViewById(R.id.button5);
        TextView result=findViewById(R.id.textView);
add.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                int x=new Integer(et1.getText().toString());
                int y=new Integer(et2.getText().toString());
                int sum=x+y;
result.setText("The Ans of"+x+"+"+y+"="+sum);
            }
        });
sub.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                int x=new Integer(et1.getText().toString());
                int y=new Integer(et2.getText().toString());
                int sub=x-y;
result.setText("The ansof"+x+"-"+y+"="+sub);
            }
        });
mul.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                int x=new Integer(et1.getText().toString());
                int y=new Integer(et2.getText().toString());
                int mul=x*y;
result.setText("The ansof"+x+"*"+y+"="+mul);
            }
        });
div.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                int x=new Integer(et1.getText().toString());
                int y=new Integer(et2.getText().toString());
                int div=x/y;
result.setText("The ansof"+x+"/"+y+"="+div);
            }
        });
    }
}

