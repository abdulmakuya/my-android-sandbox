```java

class registerNewCompany extends AsyncTask<String,String,String>{


        ProgressDialog pdialog;
        String php_response;

        @Override
        protected void onPreExecute() {
            super.onPreExecute();
            pdialog = new ProgressDialog(addNew.this);//write the actual name of the activity since this is not
            //appropiate as this is an inner class (a class inside another class)
            pdialog.setMessage("registering...");
            pdialog.setCancelable(false);
            pdialog.setIndeterminate(false);//a specific time limit
            pdialog.show();
        }

        @Override
        protected String doInBackground(String... strings) {

            try {

				/* seting up the connection and send data with url */
                // create a http default client - initialize the HTTp client

                DefaultHttpClient httpclient = new DefaultHttpClient();

                //url of the sending handler
                HttpPost httppost = new HttpPost("http://hopeoftomorrow.org/bizdirectory/register_company.php");

                ArrayList<NameValuePair> nameValuePairs = new ArrayList<NameValuePair>(3);

                //the values we need to send

                nameValuePairs.add(new BasicNameValuePair("c_name", name));
                nameValuePairs.add(new BasicNameValuePair("c_email",email));
                nameValuePairs.add(new BasicNameValuePair("c_phone",phone));
                nameValuePairs.add(new BasicNameValuePair("c_address",adress));
                nameValuePairs.add(new BasicNameValuePair("c_category",company_category));
                nameValuePairs.add(new BasicNameValuePair("c_region",region));
                nameValuePairs.add(new BasicNameValuePair("c_bio",company_bio));

                httppost.setEntity(new UrlEncodedFormEntity(nameValuePairs));
                HttpResponse response = httpclient.execute(httppost);

                InputStream inputStream = response.getEntity().getContent();

                BufferedReader rd = new BufferedReader(new InputStreamReader(inputStream), 4096);
                String line;
                StringBuilder sb = new StringBuilder();
                while ((line = rd.readLine()) != null) {
                    sb.append(line);
                }
                rd.close();
                php_response = sb.toString();
                inputStream.close();

            } catch (Exception e) {
                Toast.makeText(getApplicationContext(),"Try Again", Toast.LENGTH_LONG).show();
            }

            return php_response;

        }

        @Override
        protected void onPostExecute(String s) {
            super.onPostExecute(s);
            pdialog.dismiss();

            if (php_response.equals("1")){
                Toast.makeText(addNew.this, "Company succesfully registered", Toast.LENGTH_SHORT).show();
            }else{
                Toast.makeText(addNew.this, "Registration failed", Toast.LENGTH_SHORT).show();
        }
    }
}


```
