# Create_SingleTouchView
곡선그리기
<hr><br>
<img width="800" height="400" src="https://github.com/Bono-kim/Create_SingleTouchView/blob/master/20.PNG"/>
●Change the setContentView part of the main activity
<br>
메인 엑티비티의  setContentView 부분을 바꿔준다.
<hr><br>
●Create a SingleTouchView.java file in the src folder and put the following code in it.
<br>
다음 src폴더에 SingleTouchView.java 파일을 만들어서 아래의 코드를 넣어준다
<hr><br>

```java
package com.example.singletouch;

import android.content.Context;
import android.graphics.Canvas;
import android.graphics.Color;
import android.graphics.Paint;
import android.graphics.Path;
import android.util.AttributeSet;
import android.view.MotionEvent;
import android.view.View;

public class SingleTouchView extends View {
    private Paint paint = new Paint();
    private Path path = new Path();

    public SingleTouchView(Context context, AttributeSet attrs){
        super(context,attrs);

        paint.setAntiAlias(true); // 선분을 매끄럽게 하기위해 추가,Add to smooth line
        paint.setStrokeWidth(10f);// 선분의 두께를 10으로 한다.Let the line segment be 10
        paint.setColor(Color.MAGENTA);
        paint.setStyle(Paint.Style.STROKE);
        paint.setStrokeJoin(Paint.Join.ROUND);
    }
    @Override
    protected void onDraw(Canvas canvas){
        canvas.drawPath(path,paint); // 현재까지의 경로를 그린다.Draw the path to the present.
    }
    @Override
    public boolean onTouchEvent(MotionEvent event){
        float eventX = event.getX(); // 마우스가 터치된 위치를 얻는다.Get mouse touched location
        float eventY = event.getY();
        switch (event.getAction()){
            case MotionEvent.ACTION_DOWN:
                path.moveTo(eventX,eventY); // 터치가 눌러질떄의 경로에 위치저장, Save location in the path where touch is pressed
                return true;
            case MotionEvent.ACTION_MOVE:
                path.lineTo(eventX,eventY); // 터치가 떼어지면 경로에 직선그리기 저장.Save straight line on path when touch is released
                break;
            case MotionEvent.ACTION_UP:
                break;
            default:
                return false;
        }
        invalidate();
        return true;
    }
}

```
<hr><br>
<img width="200" height="330" src="https://github.com/Bono-kim/Create_SingleTouchView/blob/master/16.jpg"/>
●If you run it, you can draw a line on the screen as the picture above.
<br>
실행시켜주면 위의 사진처럼 화면에서 선을 그릴수있다.
<hr><br>
