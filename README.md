# Download-Images-From-Web
Download Images from Web
------------------------
* **Step 1. Construct URL by *"NSURL"*.**

        // Step1. Construct URL by NSURL
        var imgURL = NSURL(string: "http://upload.wikimedia.org/wikipedia/commons/thumb/b/b9/Steve_Jobs_Headshot_2010-CROP.jpg/220px-Steve_Jobs_Headshot_2010-CROP.jpg")
        
* **Step 2. Create URL request by *"NSURLRequest"*.**

        // Step2. Create URL request by NSURLRequest
        let urlRequest = NSURLRequest(URL: imgURL!)
        
* **Step 3. Excute request asynchrounously to show image immediately**

        // Step3. Excute request asynchrounously to make sure that image is downloaded before shown
        //        - Loads the data for a URL request and executes a handler block on an operation queue when the request completes or fails.
        NSURLConnection.sendAsynchronousRequest(urlRequest, queue: NSOperationQueue.mainQueue()) { (urlResponse, urlData, urlError) -> Void in
            if urlError != nil {
                println("Error...")
            } else {
                let image = UIImage(data: urlData)

                // +--- Store the data locally ---+
                // +------------------------------+
                // Step1. Creates a list of directory search paths.
                var paths:[AnyObject] = NSSearchPathForDirectoriesInDomains(NSSearchPathDirectory.DocumentDirectory, NSSearchPathDomainMask.UserDomainMask, true)
                // Step2. Use first searched path as data store directory
                var documentsDirectory:String?
                if paths.count > 0 {
                    documentsDirectory = paths[0] as? String
                    // Step3. Construct full path with filename
                    var savePath = documentsDirectory! + "/jobs.jpg"
                    // Step4. Save the data to the target path
                    NSFileManager.defaultManager().createFileAtPath(savePath, contents: urlData, attributes: nil)
                    
                    self.imageView.image = UIImage(named: savePath)
                }
            }
        }
        
Store/access data file on system
--------------------------------
* **Store file on system search path**

        // +--- Store the data locally ---+
        // +------------------------------+
        
        // Step1. Creates a list of directory search paths.
        var paths:[AnyObject] = NSSearchPathForDirectoriesInDomains(NSSearchPathDirectory.DocumentDirectory, NSSearchPathDomainMask.UserDomainMask, true)
                  
        // Step2. Use first searched path as data store directory
        var documentsDirectory:String?
        if paths.count > 0 {
            documentsDirectory = paths[0] as? String
                      
            // Step3. Construct full path with filename
            var savePath = documentsDirectory! + "/jobs.jpg"
                      
            // Step4. Save the data to the target path
            NSFileManager.defaultManager().createFileAtPath(savePath, contents: urlData, attributes: nil)
                      
            self.imageView.image = UIImage(named: savePath)
        }
                
* **Access data file on system search path**

        // +--- Access locally saved data ---+
        // +---------------------------------+
        
        // Step1. Creates a list of directory search paths.
        var paths:[AnyObject] = NSSearchPathForDirectoriesInDomains(NSSearchPathDirectory.DocumentDirectory, NSSearchPathDomainMask.UserDomainMask, true)
        
        // Step2. Use first searched path as data store directory
        var documentsDirectory:String?
        if paths.count > 0 {
            documentsDirectory = paths[0] as? String
            
            // Step3. Construct full path with filename
            var savePath = documentsDirectory! + "/jobs.jpg"
            
            // Step4. Access the data by using saved path
            self.imageView.image = UIImage(named: savePath)
        }
