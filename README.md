public class WarwLogin extends AppCompatActivity {
EditText editText,editText1;
Button button;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_warw_login);
        editText=findViewById(R.id.usern);
        editText1=findViewById(R.id.passn);
        button=findViewById(R.id.log);
        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                StringRequest stringRequest=new StringRequest(Request.Method.GET, "http://182.77.51.81/WMSAPI/Account/LoginUser?UserName"+editText+"&Password"+editText1, new Response.Listener<String>() {
                    @Override
                    public void onResponse(String response) {
                        Toast.makeText(getApplicationContext(),"Success"+response.toString(),Toast.LENGTH_SHORT).show();
                       
                    }
                }, new Response.ErrorListener() {
                    @Override
                    public void onErrorResponse(VolleyError error) {
                        Toast.makeText(getApplicationContext(),"not",Toast.LENGTH_SHORT).show();
                    }
                }){

                    @Override
                    protected Map<String, String> getParams() throws AuthFailureError {
                       Map<String,String>map=new HashMap<>();
                       return map;
                    }

                    @Override
                    public Map<String, String> getHeaders() throws AuthFailureError {
                        Map<String, String> headers = new HashMap<>();
                        String credentials="UserName:Password";
                        String auth = "Basic "+ Base64.encodeToString(credentials.getBytes(), Base64.NO_WRAP);
                        headers.put("Content-Type", "application/json");
                        headers.put("Authorization", auth);
                        return super.getHeaders();
////////////////////////i just try getHeader 
                    }
                };
                RequestQueue requestQueue= Volley.newRequestQueue(getApplicationContext());
                requestQueue.add(stringRequest);

            }
        });
    }
}
