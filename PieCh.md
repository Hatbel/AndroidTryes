# AndroidTryes


// Pie Chart class



package com.example.testb;

import android.annotation.SuppressLint;
import android.content.Context;
import android.graphics.Canvas;
import android.graphics.Color;
import android.graphics.Paint;
import android.graphics.RectF;
import android.view.View;

@SuppressLint("ViewConstructor")
public class PieCh extends View {
    float start = 0;
    int[] data;
    int numberOfParts;
    private int[] color;

    public PieCh(Context context, int numOfItems, int[] data, int[] color){
        super(context);
        setFocusable(true);
        this.numberOfParts = numOfItems;
        this.data = data;
        this.color = color;
    }
    @Override
    protected void onDraw(Canvas canvas){
        super.onDraw(canvas);
        canvas.drawColor(Color.WHITE);
        @SuppressLint("DrawAllocation") Paint p = new Paint();
        p.setAntiAlias(true);
        p.setStyle(Paint.Style.STROKE);
        p.setStrokeWidth(0);
        p.setStyle(Paint.Style.FILL);
        float[] scaledValues = scale();

        @SuppressLint("DrawAllocation") RectF rectF = new RectF(0,0,getWidth(),getWidth());

        p.setColor(Color.BLACK);
        for(int i = 0; i< numberOfParts; i++){
            p.setColor(color[i]);
            p.setStyle(Paint.Style.FILL);
            canvas.drawArc(rectF,start,scaledValues[i],true,p);
            start = start + scaledValues[i];
        }
    }
    private float[] scale() {
        float[] scaledValues = new float[this.data.length];
        float total = getTotal();
        for (int i = 0; i < this.data.length; i++) {
            scaledValues[i] = (this.data[i] / total) * 360;
        }
        return scaledValues;
    }
    private float getTotal(){
        float total = 0;
        for(float val:this.data)
            total+=val;
        return total;
    }

}

