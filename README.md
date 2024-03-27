# MA

package com.example.exertnal_radiobutton_checkbox;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.CheckBox;
import android.widget.RadioButton;
import android.widget.RadioGroup;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity {
    CheckBox c1,c2;
    RadioGroup rg;
    RadioButton rb;
    TextView t1,t2;
    Button submit;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        c1=findViewById(R.id.checkBox);
        c2=findViewById(R.id.checkBox2);
        rg=findViewById(R.id.radioGroup);
        rb=findViewById(R.id.radioButton);
        t1=findViewById(R.id.textView);
        t2=findViewById(R.id.textView2);
        submit=findViewById(R.id.button);
        submit.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                int selected= rg.getCheckedRadioButtonId();
                rb=findViewById(selected);
                t1.setText(rb.getText().toString());
                int total=0;
                if(c1.isChecked()){
                    total+=50;
                }
                if(c2.isChecked()){
                    total+=70;
                }
                t2.setText("Total Amount:"+total);
            }
        });


    }
}












DB

package com.example.database;


import android.app.Activity;
import android.app.AlertDialog.Builder;
import android.content.Context;
import android.database.Cursor;
import android.database.sqlite.SQLiteDatabase;
import android.os.Bundle;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.Button;
import android.widget.EditText;

public class MainActivity extends Activity implements OnClickListener
{
    EditText Rollno,Name,Marks;
    Button Insert,Delete,Update,View,ViewAll;
    SQLiteDatabase db;
    /** Called when the activity is first created. */
    @Override
    public void onCreate(Bundle savedInstanceState)
    {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Rollno=(EditText)findViewById(R.id.Rollno);
        Name=(EditText)findViewById(R.id.Name);
        Marks=(EditText)findViewById(R.id.Marks);
        Insert=(Button)findViewById(R.id.Insert);
        Delete=(Button)findViewById(R.id.Delete);
        Update=(Button)findViewById(R.id.Update);
        View=(Button)findViewById(R.id.View);
        ViewAll=(Button)findViewById(R.id.ViewAll);

        Insert.setOnClickListener(this);
        Delete.setOnClickListener(this);
        Update.setOnClickListener(this);
        View.setOnClickListener(this);
        ViewAll.setOnClickListener(this);

        // Creating database and table
        db=openOrCreateDatabase("StudentDB", Context.MODE_PRIVATE, null);
        db.execSQL("CREATE TABLE IF NOT EXISTS student(rollno VARCHAR,name VARCHAR,marks VARCHAR);");
    }
    public void onClick(View view)
    {
        // Inserting a record to the Student table
        if(view==Insert)
        {
            // Checking for empty fields
            if(Rollno.getText().toString().trim().length()==0||
                    Name.getText().toString().trim().length()==0||
                    Marks.getText().toString().trim().length()==0)
            {
                showMessage("Error", "Please enter all values");
                return;
            }

            db.execSQL("INSERT INTO student VALUES('"+Rollno.getText()+"','"+Name.getText()+
                    "','"+Marks.getText()+"');");
            showMessage("Success", "Record added");
            clearText();
        }
        // Deleting a record from the Student table
        if(view==Delete)
        {
            // Checking for empty roll number
            if(Rollno.getText().toString().trim().length()==0)
            {
                showMessage("Error", "Please enter Rollno");
                return;
            }
            Cursor c=db.rawQuery("SELECT * FROM student WHERE rollno='"+Rollno.getText()+"'", null);
            if(c.moveToFirst())
            {
                db.execSQL("DELETE FROM student WHERE rollno='"+Rollno.getText()+"'");
                showMessage("Success", "Record Deleted");
            }
            else
            {
                showMessage("Error", "Invalid Rollno");
            }
            clearText();
        }
// Updating a record in the Student table
        if(view==Update)
        {
            // Checking for empty roll number
            if(Rollno.getText().toString().trim().length()==0)
            {
                showMessage("Error", "Please enter Rollno");
                return;
            }
            Cursor c=db.rawQuery("SELECT * FROM student WHERE rollno='"+Rollno.getText()+"'", null);
            if(c.moveToFirst()) {
                db.execSQL("UPDATE student SET name='" + Name.getText() + "',marks='" + Marks.getText() +
                        "' WHERE rollno='"+Rollno.getText()+"'");
                showMessage("Success", "Record Modified");
            }
            else {
                showMessage("Error", "Invalid Rollno");
            }
            clearText();
        }
        // Display a record from the Student table
        if(view==View)
        {
// Checking for empty roll number
            if(Rollno.getText().toString().trim().length()==0)
            {
                showMessage("Error", "Please enter Rollno");
                return;
            }
            Cursor c=db.rawQuery("SELECT * FROM student WHERE rollno='"+Rollno.getText()+"'", null);
            if(c.moveToFirst())
            {
                Name.setText(c.getString(1));
                Marks.setText(c.getString(2));
            }
            else
            {
                showMessage("Error", "Invalid Rollno");
                clearText();
            }
        }
        // Displaying all the records
        if(view==ViewAll)
        {
            Cursor c=db.rawQuery("SELECT * FROM student", null);
            if(c.getCount()==0)
            {
                showMessage("Error", "No records found");
                return;}
            StringBuffer buffer=new StringBuffer();
            while(c.moveToNext())
            {
                buffer.append("Rollno: "+c.getString(0)+"\n");
                buffer.append("Name: "+c.getString(1)+"\n");
                buffer.append("Marks: "+c.getString(2)+"\n\n");
            }
            showMessage("Student Details", buffer.toString());
        }
    }
    public void showMessage(String title,String message)
    {
        Builder builder=new Builder(this);
        builder.setCancelable(true);
        builder.setTitle(title);
        builder.setMessage(message);
        builder.show();
    }
    public void clearText()
    {
        Rollno.setText("");
        Name.setText("");
        Marks.setText("");
        Rollno.requestFocus();
    }
}












FONT AND COLOR








package com.example.fontandcolor;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;

import android.graphics.Color;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import androidx.appcompat.app.AppCompatActivity;
public class MainActivity extends AppCompatActivity
{
    int ch=1;
    float font=30;
    @Override
    protected void onCreate(Bundle savedInstanceState)
    {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        final TextView t= (TextView) findViewById(R.id.textView);
        Button b1= (Button) findViewById(R.id.button);
        b1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                t.setTextSize(font);
                font = font + 5;
                if (font == 50)
                    font = 30;
            }
        });
        Button b2= (Button) findViewById(R.id.button2);
        b2.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                switch (ch) {
                    case 1:
                        t.setTextColor(Color.RED);
                        break;
                    case 2:
                        t.setTextColor(Color.GREEN);
                        break;
                    case 3:
                        t.setTextColor(Color.BLUE);
                        break;
                    case 4:
                        t.setTextColor(Color.CYAN);
                        break;
                    case 5:
                        t.setTextColor(Color.YELLOW);
                        break;
                    case 6:
                        t.setTextColor(Color.MAGENTA);
                        break;
                }
                ch++;
                if (ch == 7)
                    ch = 1;
            }
        });
    }
}



HANDLER

package com.example.handlerforcia2;

import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.os.Handler;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {
    Button btnstart, btnstop;
    TextView txtcounter;
    int i = 1;
    Handler customHandler = new Handler();
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        txtcounter = findViewById(R.id.textView);
        btnstart = findViewById(R.id.button);
        btnstop = findViewById(R.id.button2);
        btnstart.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                customHandler.postDelayed(updateTimerThread,0);
            }
        });
        btnstop.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                customHandler.removeCallbacks(updateTimerThread);
            }
        });
    }


    private final Runnable updateTimerThread = new Runnable() {
        @Override
        public void run() {
            txtcounter.setText(""+i);
            customHandler.postDelayed(this,2000);
            i++;

        }
    };
}






IMAGESWICHER

package com.example.imageswitcher;



import androidx.appcompat.app.ActionBar;
import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;
import android.view.ViewGroup;
import android.widget.Button;
import android.widget.FrameLayout;
import android.widget.ImageSwitcher;
import android.widget.ImageView;
import android.widget.ViewSwitcher;

public class MainActivity extends AppCompatActivity {
    ImageSwitcher imageSwitcher;
    Button prev, next;
    int[] image = {R.drawable.android_image, R.drawable.android_image1, R.drawable.android_image2};
    int position = 0;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        imageSwitcher = findViewById(R.id.imageSwitcher);
        prev = findViewById(R.id.button);
        next = findViewById(R.id.button2);


        imageSwitcher.setFactory(new ViewSwitcher.ViewFactory() {
            @Override
            public View makeView() {
                return null;
            }
        });

        // Setting ImageSwitcher
       imageSwitcher.setFactory(new ViewSwitcher.ViewFactory() {
            @Override
            public View makeView() {
                ImageView imageView = new ImageView(MainActivity.this);

               // imageView.setScaleType(ImageView.ScaleType.FIT_CENTER);
                return imageView;
            }
        });

        prev.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                changeImage(-1);
            }
        });

        next.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                changeImage(1);
            }
        });
    }

    // Method to change image in the ImageSwitcher
    private void changeImage(int direction) {
        position = (position + direction + image.length) % image.length;
        imageSwitcher.setImageResource(image[position]);
    }
}




IMAGEANIMATIO



package com.example.annimationforcia2;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;
import android.animation.ObjectAnimator;
import android.view.animation.Animation;
import android.view.animation.LinearInterpolator;
import android.view.animation.RotateAnimation;
import android.view.animation.ScaleAnimation;
import android.view.animation.TranslateAnimation;
import android.widget.Button;
import android.widget.ImageView;

public class MainActivity extends AppCompatActivity {
    Button b1,b2,b3,b4;
    ImageView img;
    ScaleAnimation scale;
    TranslateAnimation translate;

    RotateAnimation rotate;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        b1=findViewById(R.id.button);
        b2=findViewById(R.id.button2);
        b4=findViewById(R.id.button4);
        img=findViewById(R.id.imageView);
        b1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                scale=new ScaleAnimation(0,2,0,2);
                scale.setDuration(2000);
                img.startAnimation(scale);
            }
        });
        b2.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                rotate = new RotateAnimation(0, 360,
                        Animation.RELATIVE_TO_SELF, 0.5f,
                        Animation.RELATIVE_TO_SELF, 0.5f);
                rotate.setDuration(1000);
                rotate.setRepeatCount(10);
                img.startAnimation(rotate);
            }
        });
        b4.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                translate=new TranslateAnimation(0,-500,0,400);
                translate.setDuration(1000);
                img.startAnimation(translate);
            }
        });

    }

}





PRIMITIVE



package com.example.cia_primitive;

import androidx.appcompat.app.AppCompatActivity;

import android.graphics.Bitmap;
import android.graphics.Canvas;
import android.graphics.Color;
import android.graphics.Paint;
import android.graphics.drawable.BitmapDrawable;
import android.os.Bundle;
import android.widget.ImageView;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Bitmap bg = Bitmap.createBitmap(720,1280, Bitmap.Config.ARGB_8888);

        ImageView i =(ImageView) findViewById(R.id.imageView);
        i.setBackgroundDrawable(new BitmapDrawable(bg));
        Canvas canvas = new Canvas(bg);
        Paint paint = new Paint();
        paint.setColor(Color.BLUE);
        paint.setTextSize(80);

        canvas.drawText("Circle",150,140,paint);
        canvas.drawCircle(300,420,250,paint);

        canvas.drawText("Rectangle",150,900,paint);
        canvas.drawRect(150,950,1500,1500,paint);


        canvas.drawText("Line",550,150,paint);
        canvas.drawLine(550,850,1550,900,paint);





    }
}






ARITHMETIC



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





CONCATENATION

package com.example.textcon;

import androidx.appcompat.app.AppCompatActivity;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import android.os.Bundle;

public class MainActivity extends AppCompatActivity {
EditText name, lastname, mobile;
TextView details;
    Button click;
booleanisAllFieldsChecked = false;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
super.onCreate(savedInstanceState);
setContentView(R.layout.activity_main);
        name = (EditText) findViewById(R.id.editTextTextPersonName);
lastname = (EditText) findViewById(R.id.editTextTextPersonName2);
        mobile = (EditText) findViewById(R.id.editTextTextPersonName3);
        click = (Button) findViewById(R.id.button4);
        details = (TextView) findViewById(R.id.textView);
click.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
isAllFieldsChecked = CheckAllFields();
                if (isAllFieldsChecked)
details.setText("Name: " + name.getText() + lastname.getText() + "\nMobile: " + mobile.getText() );
            }
        });
    }

    private booleanCheckAllFields() {
        int err = 0;
        if (name.length() == 0) {
name.setError("This field is required");
            err += 1;
        }
        if (lastname.length() == 0) {
lastname.setError("This field is required");
            err += 1;
        }
        if (mobile.length() == 0) {
mobile.setError("This field is required");
            err += 1;
        }
        if (err == 0)
            return true;
        else
            return false;
    }
}






ARITHMETIC


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


