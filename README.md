# Uexpenses
Self project created before starting clases at York Univeristy

package com.greg.app.uexpenses;

import android.app.Activity;
import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.AdapterView;
import android.widget.AdapterView.OnItemSelectedListener;
import android.widget.ArrayAdapter;
import android.widget.ImageView;
import android.widget.Spinner;
import android.widget.ToggleButton;

public class uExpenses extends Activity {
	private Spinner mRegularSpinner, mExtraSpinner;
	private ToggleButton mHome, mPersonal, mCar;
	private ImageView mHomeImage, mPersonalImage, mCarImage;
	private static final int ACTIVITY_EXPENSE_ENTRY = 0;
	private static final int ACTIVITY_GRAFICAS =1;
	public static final String CATEGORY = "whichCategory";
	public static final String DESCRIPTION = "whichDescription";
	public static final String HOME_BILLS = "Home Bills";
	public static final String HOME_EXTRAS= "Home Extras";
	public static final String PERSONAL_BILLS_AND_PAYMENT = "Personal Bills";
	public static final String PERSONAL_EXTRAS = "Personal Extras";
	public static final String CAR_BILLS_AND_PAYMENTS = "Car Bills";
	public static final String CAR_EXTRAS = "Car Extras";
	private String mDescription;
    /** Called when the activity is first created. */
    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main);
        mHomeImage = (ImageView) findViewById(R.id.imageofHome);
        mPersonalImage = (ImageView) findViewById(R.id.imageofPersonal);
        mCarImage = (ImageView) findViewById(R.id.imageofCar);
        mHome = (ToggleButton) findViewById(R.id.homeToggle);
        mPersonal = (ToggleButton) findViewById(R.id.personalToggle);
        mCar = (ToggleButton) findViewById(R.id.carToggle);
        mRegularSpinner = (Spinner) findViewById(R.id.regular);
        mExtraSpinner = (Spinner) findViewById(R.id.extra);
        if(mPersonal.isChecked()){
        	mPersonal.performClick();
        }
        else if(mCar.isChecked()){
        	mCar.performClick();
        }
        else{
        	mHome.setChecked(true);
        	ArrayAdapter<CharSequence> regularAdapter = ArrayAdapter.createFromResource(this, R.array.home_montly_bills_empty, android.R.layout.simple_spinner_item);
    		regularAdapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item);
    		mRegularSpinner.setAdapter(regularAdapter);
    		ArrayAdapter<CharSequence> extraAdapter = ArrayAdapter.createFromResource(this, R.array.home_extras_empty, android.R.layout.simple_spinner_item);
    		extraAdapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item);
    		mExtraSpinner.setAdapter(extraAdapter);
        }		
		mRegularSpinner.setOnItemSelectedListener(new regularSelection());		
		mExtraSpinner.setOnItemSelectedListener(new extraSelection());
        mHome.setOnClickListener(new View.OnClickListener() {
			
			//@Override
			public void onClick(View v) {
				// TODO Auto-generated method stub
				mHome.setChecked(true);
				mPersonal.setChecked(false);
				mCar.setChecked(false);
				mPersonalImage.setImageResource(R.drawable.ic_person_unchecked);
				mCarImage.setImageResource(R.drawable.ic_launcher_caruncheked);
				mHomeImage.setImageResource(R.drawable.ic_house_checked);
				ArrayAdapter<CharSequence> regularAdapter = ArrayAdapter.createFromResource(uExpenses.this, R.array.home_montly_bills_empty, android.R.layout.simple_spinner_item);
				regularAdapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item);
				mRegularSpinner.setAdapter(regularAdapter);
				ArrayAdapter<CharSequence> extraAdapter = ArrayAdapter.createFromResource(uExpenses.this, R.array.home_extras_empty, android.R.layout.simple_spinner_item);
				extraAdapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item);
				mExtraSpinner.setAdapter(extraAdapter);
			}
		});
        mPersonal.setOnClickListener(new View.OnClickListener() {
			
			//@Override
			public void onClick(View v) {
				// TODO Auto-generated method stub
				mHome.setChecked(false);
				mPersonal.setChecked(true);
				mCar.setChecked(false);
				mPersonalImage.setImageResource(R.drawable.ic_person_checked);
				mCarImage.setImageResource(R.drawable.ic_launcher_caruncheked);
				mHomeImage.setImageResource(R.drawable.ic_house_unchecked);
				ArrayAdapter<CharSequence> regularAdapter = ArrayAdapter.createFromResource(uExpenses.this, R.array.personal_bills_empty, android.R.layout.simple_spinner_item);
				regularAdapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item);
				mRegularSpinner.setAdapter(regularAdapter);
				ArrayAdapter<CharSequence> extraAdapter = ArrayAdapter.createFromResource(uExpenses.this, R.array.personal_extras_empty, android.R.layout.simple_spinner_item);
				extraAdapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item);
				mExtraSpinner.setAdapter(extraAdapter);
			}
		});
        mCar.setOnClickListener(new View.OnClickListener() {
			
			//@Override
			public void onClick(View v) {
				// TODO Auto-generated method stub
				mHome.setChecked(false);
				mPersonal.setChecked(false);
				mCar.setChecked(true);
				mPersonalImage.setImageResource(R.drawable.ic_person_unchecked);
				mCarImage.setImageResource(R.drawable.ic_launcher_carchecked);
				mHomeImage.setImageResource(R.drawable.ic_house_unchecked);
				ArrayAdapter<CharSequence> regularAdapter = ArrayAdapter.createFromResource(uExpenses.this, R.array.car_bills_empty, android.R.layout.simple_spinner_item);
				regularAdapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item);
				mRegularSpinner.setAdapter(regularAdapter);
				ArrayAdapter<CharSequence> extraAdapter = ArrayAdapter.createFromResource(uExpenses.this, R.array.car_extras_empty, android.R.layout.simple_spinner_item);
				extraAdapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item);
				mExtraSpinner.setAdapter(extraAdapter);
			}
		});
    }
    @Override
    protected void onPause() {
        super.onPause();
        //saveState();
    }

    @Override
    protected void onResume() {
        super.onResume();
        if(mPersonal.isChecked()){
        	mPersonal.performClick();
        }
        else if(mCar.isChecked()){
        	mCar.performClick();
        }
        else{
        	mHome.performClick();
        }
    }
    public void openGraficas(View v){
    	Intent i = new Intent(this, Graficas.class);
    	startActivityForResult(i, ACTIVITY_GRAFICAS);
    }
    public class regularSelection implements OnItemSelectedListener {
		public void onItemSelected(AdapterView<?> parent, View view, int pos, long id){
			mDescription = parent.getItemAtPosition(pos).toString();
			if(mDescription.compareTo("REGULAR: Select an item")!=0){
				if(mHome.isChecked()){
		    		Intent i = new Intent(uExpenses.this, PersonalExpenses.class);
		       	 	i.putExtra(CATEGORY, HOME_BILLS);
		       	 	i.putExtra(DESCRIPTION, mDescription);
		            startActivityForResult(i, ACTIVITY_EXPENSE_ENTRY);
		    	}
		    	else if(mPersonal.isChecked()){
		    		Intent i = new Intent(uExpenses.this, PersonalExpenses.class);
		       	 	i.putExtra(CATEGORY, PERSONAL_BILLS_AND_PAYMENT);
		       	 	i.putExtra(DESCRIPTION, mDescription);
		            startActivityForResult(i, ACTIVITY_EXPENSE_ENTRY);
		    	}
		    	else{
		    		Intent i = new Intent(uExpenses.this, PersonalExpenses.class);
		       	 	i.putExtra(CATEGORY, CAR_BILLS_AND_PAYMENTS);
		       	 	i.putExtra(DESCRIPTION, mDescription);
		            startActivityForResult(i, ACTIVITY_EXPENSE_ENTRY);
		    	}
			}
		}
		public void onNothingSelected (AdapterView<?> parent){
			
		}
	}
    public class extraSelection implements OnItemSelectedListener {
		public void onItemSelected(AdapterView<?> parent, View view, int pos, long id){
			mDescription = parent.getItemAtPosition(pos).toString();
			if(mDescription.compareTo("EXTRA: Select an item")!=0){
				if(mHome.isChecked()){
		    		Intent i = new Intent(uExpenses.this, PersonalExpenses.class);
		       	 	i.putExtra(CATEGORY, HOME_EXTRAS);
		       	 	i.putExtra(DESCRIPTION, mDescription);
		            startActivityForResult(i, ACTIVITY_EXPENSE_ENTRY);
		    	}
		    	else if(mPersonal.isChecked()){
		    		Intent i = new Intent(uExpenses.this, PersonalExpenses.class);
		         	i.putExtra(CATEGORY, PERSONAL_EXTRAS);
		         	i.putExtra(DESCRIPTION, mDescription);
		            startActivityForResult(i, ACTIVITY_EXPENSE_ENTRY);
		    	}
		    	else{
		    		Intent i = new Intent(uExpenses.this, PersonalExpenses.class);
		        	i.putExtra(CATEGORY, CAR_EXTRAS);
		        	i.putExtra(DESCRIPTION, mDescription);
		            startActivityForResult(i, ACTIVITY_EXPENSE_ENTRY);
		    	}
			}
		}
		public void onNothingSelected (AdapterView<?> parent){
			
		}
	}
    public void selectHome(View v){
    	mHome.performClick();
    }
    public void selectPersonal(View v){
    	mPersonal.performClick();
    }
    public void selectCar(View v){
    	mCar.performClick();
    }
    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent intent) {
        super.onActivityResult(requestCode, resultCode, intent);
        //Bundle extras = intent.getExtras();
        switch(requestCode) {
            case ACTIVITY_EXPENSE_ENTRY:
            	if(mHome.isChecked()){
		    		mHome.performClick();
		    	}
		    	else if(mPersonal.isChecked()){
		    		mPersonal.performClick();
		    	}
		    	else{
		    		mCar.performClick();
		    	}
            	break;
            case ACTIVITY_GRAFICAS:
            	if(mHome.isChecked()){
		    		mHome.performClick();
		    	}
		    	else if(mPersonal.isChecked()){
		    		mPersonal.performClick();
		    	}
		    	else{
		    		mCar.performClick();
		    	}
        }
    }
}
