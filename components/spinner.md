```java

public void  displaySpinner(){

        //create string
        final String [] categories_names = {"General","Informarion technology","Mining",
                "Travel tourism","Healthcare","Food processing","Agriculture","Microfinace"};

        Spinner spinnerCategory = findViewById(R.id.spinnerCategory);

        ArrayAdapter<String> categoryAdapter = new ArrayAdapter<String>(addNew.this,
                android.R.layout.simple_spinner_item,
                categories_names
        );
        spinnerCategory.setAdapter(categoryAdapter);

        spinnerCategory.setOnItemSelectedListener(new AdapterView.OnItemSelectedListener() {
            @Override
            public void onItemSelected(AdapterView<?> adapterView, View view, int position, long l) {
               company_category = categories_names[position] ;
            }

            @Override
            public void onNothingSelected(AdapterView<?> adapterView) {
                company_category = categories_names[0];
                //company_category = "General";
            }
        });

```
