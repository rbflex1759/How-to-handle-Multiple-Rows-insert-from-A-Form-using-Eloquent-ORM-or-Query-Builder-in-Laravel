# How-to-handle-Multiple-Rows-insert-from-A-Form-using-Eloquent-ORM-or-Query-Builder-in-Laravel


Step1: create HTML form to submit array like: 

<input type="text"   name="refereename[]"/>
<input type="text"   name="refereelocation[]"/> 
<input type="text" name="refereecompany[]"/>
<input type="text" name="refereephone[]"/>
<input type="text" name="refereeemail[]"/>  
<input type="text" name="relationship[]"/>  

Step2: Create a model class if you want to use Eloquent ORM like this:

Php artisan make:model Employeereferees
Edit the model class, edit tbale name and add fillable columns to the model.

Step3: Create a controller and add this to the top of the page:

use db; // if you are using Query Builder.
use App\Models\ Employeereferees; // if you are using Eloquent ORM.
Use Carbon\carbon; //if you want to use date 
Next, add this function to the controller:
public function addReferees(Request $request)
{
       $employeeID =  mt_rand(100000, 999999);
        $date  = Carbon::now()->format('Y-m-d');
foreach($request->refereename as $i =>$value)
     	 {
        $referees[]=[
            'employeeId'=>$employeeId,
            'refereename'=>$request->refereename[$i],
            'refereecompany'=>$request->refereecompany[$i],
            'refereephone'=>$request->refereephone[$i],
            'refereeemail'=>$request->refereeemail[$i],
            'relationship'=>$request->relationship[$i],
            'refereelocation'=>$request->refereelocation[$i],
            'created_at'=>$date,
            'updated_at'=>$date,
            ];
      }
//use only one option here:
      DB::table('hrms_referees')->insert($referees); // if you are using Query Builder approach 
      EmployeeReferees::insert($referees);//if you are using eloquent approach
       return back()->with('success','Submission Successful');
}

