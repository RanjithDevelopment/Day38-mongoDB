# Day38-mongoDB
1.Find all the topics and tasks which are thought in the month of October
    
    db.Topics.aggregate(
    [
        {
            $lookup: {
                from: 'Tasks',
                localField : 'complete',
                foreignField: 'complete',
                as: 'qusNo1'
            },
          
        },
         { $match: {
                complete:'October'
            }
          }
    ]
)
    
  2.  Find all the company drives which appeared between 15 oct-2020 and 31-oct-2020
 db.Company_drives.find({date:{$gte:'15 oct-2020',$lte:'31 oct-2020'}});
 
  3. Find all the company drives and students who are appeared for the placement.
 db.Company_drives.aggregate(
    [
        {
            $lookup: {
                from: 'Students',
                localField : 'company_id',
                foreignField: 'company_id',
                as: 'qusNo3'
            }
        }
    ]
)
  4. Find the number of problems solved by the user in codekata
  db.CodeKata.aggregate([
        {
            $project: {
                _id : 0,
                   
                submitted :1
            }
        }
    ])
   5 . Find all the mentors with who has the mentee's count more than 15  
    db.mentor.aggregate([
        {
            $project: { 
                mentor_id : 1,
              	MentorName : 1,
	            course : 1,
                count: { $size:"$student_ids" }
                
            }
            
        },{
            $match: {
                count:13
              }
            
        }
     ])
    6. Find the number of users who are absent and task is not submitted  between 15 oct-2020 and 31-oct-2020
      db.Attenance.aggregate(
    [
            {
             $match: {absent:{$gte:'15 oct-2020',$lt:'31 oct-2020'}}
          }
      
    ]
)
