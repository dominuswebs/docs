# Terminal

    Arguments are given when the program starts (grep hello file.txt).

        Command:

            grep hello file.txt
        
        file.txt contents:

            hello world
            foo bar
            hello again
    
        What happens:

            grep takes hello as an argument (pattern to search)

            grep also takes file.txt as an argument (file to read)

            It searches the file directly and prints matching lines.

        Result:
            hello world
            hello again

    Pipe sends data after start (cat file.txt | grep hello).

        Command:
            
            cat file.txt | grep hello
        
        file.txt contents:

            hello world
            foo bar
            hello again
        
        What happens:

            cat file.txt sends file contents to stdout

            | pipes that output to grep hello, which reads it via stdin

            grep searches for hello in that incoming stream.

        Result:

            hello world
            hello again

        Both Arguments/Pipe produce the same output here, but:

            The argument version is usually more efficient (fewer processes).
            The pipe version is more flexible (you can chain multiple commands).

    List all Processes

        lsof -i

    Find which process is using port 3000

        sudo lsof -i :3000

    Kill a process

        kill -9 <PID>

    Find previous commands (bck-i-search)

        ctrl + r

    Command substitution $() - runs the command inside the parentheses and replaces it with its output.

        rm $(ls | grep '\.log$') 

        How it works:

            ls – lists files in the current directory.
            grep '\.log$' – filters files ending in .log.
            $(...) – substitutes the filtered list as arguments to rm.

    Search for a string inside files. Only search in folders whose names start with abc_. Get a list of folder names (not file names) that contain at least one matching file.

        rg "your_search_string" --files-with-matches -g "abc_*/**" | cut -d'/' -f1 | sort -u


# Docker

	Testing environment - workspace/_projects/docker

	Tutorial - https://docs.docker.com/get-started/introduction/

	Mac/Win - use Docker desktop
	Linux - CLI is enough

	Using Docker Desktop


	Build

		Command line always run from parent directory where Dockerfile is. Update any paths in Dockefilr and compose.yaml

	

	Errors and bugs

	Error:

		Error response from daemon: Ports are not available: exposing port TCP 0.0.0.0:80 -> 0.0.0.0:0: listen tcp 0.0.0.0:80: bind: address already in use

	Fix:

		Update compose.yml if useing traefik

	Guides:

		PHP, NGINX, MariaDB - https://medium.com/@tech_18484/deploying-a-php-web-app-with-docker-compose-nginx-and-mariadb-d61a84239c0d


    




# GIT

Using different git accounts

	This only sets the author for commit

	git config --local user.email "yourmail@example.com"

    To handle multiple accounts set an ssh config with different hosts like this

        Host github_personal
            HostName github.com
            AddKeysToAgent yes
            UseKeychain yes
            IdentityFile ~/.ssh/keys/id_ed25519
            IdentitiesOnly yes

        Host github_ditt
            HostName github.com
            AddKeysToAgent yes
            UseKeychain yes
            IdentityFile ~/.ssh/keys/id_ed25519_ditt
            IdentitiesOnly yes
    
    Then set the remote with the correct host

        git remote set-url origin git@github_personal:dominuswebs/projects.git 


	# Generate SSH keys

	Open your terminal / CMD PROMPT and type the following command:

	```
	ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
	```

	The command will ask ssh to generate a key for you. After running the command, you will see the following feedback:

	```
	Generating public/private rsa key pair.
	```

	The next line you will see would be:

	```
	Enter file in which to save the key (/Users/sprlwrks/.ssh/id_rsa): 
	```

	Here, you can specify a directory and filename for the ssh key that will be generated. The default is `/Users/sprlwrks/.ssh/id_rsa`. It will be saved in `/Users/sprlwrks/.ssh/` with the file name `id_rsa`.
	It will generate two files. `id_rsa` and `id_rsa.pub`. The `id_rsa.pub` contains your public key which you will use, you can give this to your team leader or to other people that you want. The `id_rsa` is the private key, __don't want to give this key to anyone__.

	In this case, since we are going to generate two ssh keys, we don't want to keep the default file name, set it to whatever name you want by giving it `/Users/sprlwrks/.ssh/file_name`. I named mine `id_rsa_personal`.

	The next line you will see would be:

	```
	Enter passphrase (empty for no passphrase): 
	```

	If you type a passphrase here, you will have to remember that and type the same passphrase again everytime you use this key. I'll leave it up to you to decide. For me, I did not add any passphrase so I simply pressed enter. The next line would ask you to retype the passphrase again, of course if you left it empty then just press enter.

	With all that you should have gotten something that looks like this:

	```
	aprilmintacpineda-MacBook-Pro:PWA-W88 aprilmintacpineda$ ssh-keygen -t rsa -b 4096 -C "me@example.com"
	Generating public/private rsa key pair.
	Enter file in which to save the key (/Users/sprlwrks/.ssh/id_rsa): /Users/sprlwrks/.ssh/id_rsa_personal
	Enter passphrase (empty for no passphrase): 
	Enter same passphrase again: 
	Your identification has been saved in /Users/sprlwrks/.ssh/id_rsa_personal.
	Your public key has been saved in /Users/sprlwrks/.ssh/id_rsa_personal.pub.
	The key fingerprint is:
	0b:0a:9f:58:2d:c8:a3:87:f7:44:17:f6:2c:d8:b7:3a me@example.com
	The key's randomart image is:
	+--[ RSA 4096]----+
	|                 |
	|                 |
	|      o          |
	| . . = +         |
	|  = = * S        |
	| o B = + o       |
	|o + =   o        |
	| o o  E.         |
	|    . ..         |
	+-----------------+
	```

	That's your first key. Now run `cd ~/.ssh` and then run `ls`. `ls` would list all files in the directory. You should see the keys that have been generated.

	```
	id_rsa_personal			id_rsa_personal.pub
	```

	Now try to generate another one by following the same procedure again. I named my second key `id_rsa_work`. Once you're done you should have the following files (respective to the filename you gave it):

	```
	id_rsa_personal			id_rsa_personal.pub			id_rsa_work			id_rsa_work.pub
	```

	# Adding ssh keys to github accounts (or whatever you use)

	First, I'll add my `id_rsa_personal` ssh key.

	#### 1

	Go to your github account then go to `settings -> SSH and GPG keys`. Click on `New SSH key` button.

	#### 2

	Go to your terminal again and run this command: `cat ~/.ssh/<yourfilename>.pub` replacing `<yourfilename>` with whatever file name you gave it, in this case mine is `id_rsa_personal.pub`.

	After running the commands above, you'll see something like this:

	```
	ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCha2J5mW3i3BgtZ25/FOsxywpLVkx1RgmZunIACBxV5V1lUm9I6J8uP8sP4xst/WwTWzjUY8svey1FRSNghOwtZvYZyD7lEy4FCdTn3InbRq4xXHNSVEdpG0Bbr1MEr/QWin/Q87oabQZo3wyRRJ3KjsO9xCDcwH8xcxUM+I4f3b5zSulpArjBsjkkkMsXih7L35FtzrW241mKjoA5g9/cfbqF7F6Gqwi23eUMCxwbEjgsUdFAKNbSmf9b4b7dAmfwjljM23m6FYGN75r72RH5bSuSoPdNfRwbqtHmvY0dPjcsnBRAkVokNPnvUXx4FMe7ra7T2vFOjfuyrHNVNi82TiOKRbtSxzReyNUOtpAukw833iy0hLyDy/Oo4/9aFXQEg4QSFdb/cZcTUdKE2XWIlstGApXgoy19VfJHJLjFZ7QRQQbd+8l53bZ0vUqpWINpf1UwpgKLLuCKWMqXUlaTfWSTLS+7LAM9PhsSD8FmzwFMJiSlC6ZYmT5W8c74SxRrw0EB8u/UA2UdWaOB7bj66aydOt8i+tu5HhB5eNQGDUh/19seW+48f6Qf5kcwcO/KlEn9hujJbCZA8owbzyT0KFjo5slnvEtH46EKGlaWOrRk4nuDoi3nF87TkLB8yedVxki2dvh8dmTLgGU0Dzb8NpZ+6gq3X+xnXqo92989tQ== me@example.com
	```

	#### 3

	Copy paste that to the key on your `new ssh key form` then give it whatever title you like. I gave mine `macbook`.

	#### 4

	Done! Now you have added your first ssh key to your github account, now add the other one to another github account or to the same github account giving it a different title so you can differentiate between the two.

	# Configure SSH

	#### 1

	On your terminal / CMD PROMPT, run this command: `touch ~/.ssh/config` this will create a file with the file name of `config` on the `~/.ssh` folder. Now Go to that folder and open that file with your text editor of choice.

	#### 2

	Copy paste the following on it:

	```
	Host gh_work
	    HostName github.com
	    IdentityFile ~/.ssh/id_rsa_personal
	```

	The `Host` is how you would referrence this credentials on your terminal. The `HostName` is whatever platform you use, in this case `github.com`. The `IdentityFile` is the `ssh key` to be used for this credential.

	Now add another one. By the end you should have something like these:

	```
	Host gh_work
	    HostName github.com
	    IdentityFile ~/.ssh/id_rsa_work

	Host gh_personal
	    HostName github.com
	    IdentityFile ~/.ssh/id_rsa_personal
	```

	# Testing connection

	On your terminal / CMD PROMPT, run `ssh -T git@<myHost>` replacing `myHost` with the host you wrote on the `config` file. Mine is `ssh -T git@id_rsa_personal`.

	After running that command, you should see something like this: `Hi <username>! You've successfully authenticated, but GitHub does not provide shell access.`. Now you know it's working. Go ahead and test the other key you added.

	# Cloning repository using a specific ssh key

	For this example I will clone this repository: https://github.com/aprilmintacpineda/chat-with-people-backend. To test if yours keys work, you should your own test repository.

	Run `git clone git@<myHost>:aprilmintacpineda/chat-with-people-backend.git`. Replacing myHost with the `Host` you want that was specified on your `config`. Ones it's done, you can run `git remote -v` and you'll see something like this:

	```
	origin	git@gh_personal:aprilmintacpineda/chat-with-people-backend.git (fetch)
	origin	git@gh_personal:aprilmintacpineda/chat-with-people-backend.git (push)
	```

	You see now that it would use my `gh_personal` keys everytime. Now make changes and commit and push the changes. If all worked well you should get no errors.

	Note that if you already have an existing clone in your machine, you can do this:

	```
	git remote add origin git@<myHost>:aprilmintacpineda/chat-with-people-backend.git
	```

	then simply push to that remote.

	Now you're all set, you can test the other key too!

	# Other Resources

	- https://help.github.com/articles/connecting-to-github-with-ssh/
	- https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/

	Permission denied error ( keys exist ) - add the private keys to user agent ssh-add ~/.ssh/path/to/private_key


	# ignoring files locally ( without using .gitignore)

	The $GIT_DIR/info/exclude file is used to specify patterns for files and directories that should be ignored by Git, similar to .gitignore, but with a few key differences:

Location: The exclude file is located inside the .git directory in your repository. Specifically, it's in the info subdirectory of the Git directory, which is typically $GIT_DIR/info/exclude. You can also think of this as .git/info/exclude.

Scope: The exclude file is specific to your local repository and does not get committed or shared with others. This makes it useful for ignoring files that are specific to your local environment but shouldn't be shared (like local configuration files, editor backups, etc.).

Usage: The file contains patterns that match files and directories you want Git to ignore. These patterns follow the same syntax as .gitignore files.

How to use $GIT_DIR/info/exclude:
Navigate to your repository: First, ensure you're in your Git repository.

bash
Copy
cd /path/to/your/repository
Open the exclude file: You can directly open and edit the exclude file:

bash
Copy
nano .git/info/exclude
Or, if you're using a different editor, substitute nano with your editor of choice (e.g., vim, code, etc.).

Add patterns: Inside the file, add the patterns for files or directories you want Git to ignore. For example:

bash
Copy
# Ignore IDE settings
.idea/
*.iml

# Ignore OS-specific files
.DS_Store
Thumbs.db

# Ignore log files
*.log
Save and close: After editing the exclude file, save it and close your editor.

Example:
Let’s say you want to ignore:

The .DS_Store file, which macOS creates in directories.
Log files with the .log extension.
The .idea/ directory created by JetBrains IDEs.
Your $GIT_DIR/info/exclude would look like:

bash
Copy
# Ignore macOS system files
.DS_Store

# Ignore JetBrains IDE project files
.idea/

# Ignore all log files
*.log
Key Points:
Local scope: This file is not shared with others, so it’s great for ignoring local files like editor settings or system-specific files.
Similar to .gitignore: The syntax is the same, and you can use glob patterns (e.g., *.log to ignore all .log files).




# JAVA


## JS

    Loops

        Loop Type	        Waits for await?	    Execution Style

        for...of	        ✅ Yes	               Sequential (if used with await)
        .forEach()	        ❌ No	               Parallel (does not wait)
        for (classic)	    ✅ Yes	               Sequential (when using await)   

        When you use for...of inside an async function, you can await each operation one at a time.

        Each await pauses the loop until the async operation finishes.

        The next iteration starts only after the previous one finishes.

        This is ideal for scenarios like:

            Network operations

            Puppeteer/Playwright scripts

            Rate-limited APIs

        forEach ignores await

            even if we write:

                someArray.forEach(async (value) => {
                    await someAsyncOperation(value);
                });
            
            It looks okay, but it's misleading:

                The async callback returns a Promise, but forEach doesn't wait for it, it just keep looping.

                The main function doesn't wait either.

                Everything runs in parallel (often too fast for controlled environments so it doesn't guarantee order).

    Electron

        When you run electron with express . from the terminal, it works because:

            You're in your project folder

            All the files (like /public) are directly accessible

            The Express server starts and serves static files

        But when bundled:

            The app is extracted into a temporary location during runtime

            Paths like __dirname + '/public' no longer point to where your static assets are

            If your server uses express.static() to serve files, it can't find them

        Preload.js

            Renderer listens for a signal from main / ipcRenderer.on(...) / You want to receive an event
            Renderer sends a signal to main / ipcRenderer.send(...) / You want to trigger an event

    NODE

        require.main is a Node-specific global reference.

            It points to the module that was executed directly with node, i.e. the entry point of your program. 

        require.main === module is a Node.js pattern that checks: Is this file being run directly? Or is it being require()d by another script (like an Electron main.js)?

            Example, app.js file that exports "myFunc":

                // all the requires

                function myFunc() {...code }

                if (require.main === module) {
                    myFunction();
                }

                modules.exports = myFunc

        const { app: electronApp } = require('electron'); is the same as this const electron = require('electron'); const electronApp = electron.app;

            We rename it in case we already have a variable with the name app. Example:

                const app = express();
                const { app: electronApp } = require('electron');

        In Node.js (CommonJS):
        You use module.exports and require():

            // file: math.js
            function add(a, b) {
            return a + b;
            }
            module.exports = add;

            // file: app.js
            const add = require('./math');
            console.log(add(2, 3)); // 5
        
        In ES Modules (Newer JavaScript):
        You use export and import:

            // file: math.mjs or with "type": "module" in package.json
            export function add(a, b) {
                return a + b;
            }

            // file: app.mjs
            import { add } from './math.mjs';
            console.log(add(2, 3)); // 5
    JSDoc

        It's a structured comment format used to describe:

            function parameters

            return types

            purpose

            usage details
    
        Syntax example:

            /**
            * Adds two numbers together.
            *
            * @param {number} a - The first number.
            * @param {number} b - The second number.
            * @returns {number} The sum of the two numbers.
            */
            function add(a, b) {
                return a + b;
            }

        Params list

            @param {string} name	A string parameter named name.
            @param {number} count	A number parameter named count.
            @param {boolean} isActive	A boolean flag.
            @param {Object} config	An object parameter.
            @param {Array} list	An array (any type of elements).
            @param {Array<string>} names	An array of strings.
            @param {function} callback	A function parameter.
            @param {*} value	Any type (wildcard).
            @param {string[]} tags	An array of strings (alternative syntax).
            @param {{x: number, y: number}} point	An object with specific shape.

        Advanced usage

            Optional parameters
            
                Use square brackets

                @param {string} [username] Optional username.
                @param {string} [role="user"] Role with default value.

                ex:

                    /**
                    * Creates a user profile.
                    *
                    * @param {string} [username] Optional username.
                    * @param {string} [role="user"] Role with default value.
                    * @returns {object} User profile object.
                    */
                    function createUser(username, role = "user") {
                        return {
                            username: username || "guest",
                            role: role,
                        };
                    }
            
            Nullable/Non-Nullable

                @param {?string} name Name can be string or null.
                @param {!Object} user User object must not be null.

            Rest Parameters

                @param {...number} values Variable number of numeric arguments.

            Generics/Type Parameters

                @param {Array.<number>} nums Array of numbers.
                @param {Promise<string>} result A promise that resolves to a string.

                ex:

                    /**
                    * Processes an array of numbers and returns a Promise resolving to a string result.
                    *
                    * @param {Array.<number>} nums Array of numbers.
                    * @param {Promise<string>} result A promise that resolves to a string.
                    * @returns {Promise<string>} A promise that resolves to a processed string.
                    */
                    function processNumbers(nums, result) {
                    return result.then(str => {
                        const sum = nums.reduce((acc, n) => acc + n, 0);
                        return `Result: ${str}, Sum: ${sum}`;
                    });
                    }

                    // Example usage:
                    const numbers = [1, 2, 3, 4];
                    const promiseString = Promise.resolve("Success");

                    processNumbers(numbers, promiseString).then(console.log);





# PHP

Generators

Sure! A generator in programming, especially in PHP, is a special type of function that allows you to iterate over a sequence of values lazily, one at a time, without having to store all the values in memory at once.

Key Concepts of Generators:
Yielding Values: Instead of returning a result all at once (like a normal function does), a generator yields values one by one. The yield keyword is used inside the generator function to "pause" the function's execution and send back a value to the caller.

Lazy Evaluation: Generators are lazy, meaning they don’t compute or return all the values upfront. They only generate the next value when it is requested, which can be more memory efficient, especially when working with large data sets.

State Preservation: When a generator yields a value, it pauses execution, and when the next value is requested, it resumes from where it left off, preserving its internal state (like local variables, loops, etc.).

Iterating Through Values: A generator returns an iterable object (in PHP, this is a Generator object). You can loop through the values using foreach or use functions like current(), next(), etc.

Example of How Generators Work:
Let’s say you have a function that generates a sequence of numbers:


function countUpTo($max) {
    $i = 1;
    while ($i <= $max) {
        yield $i; // Pauses here and yields the current value of $i
        $i++;     // Increments $i for the next iteration
    }
}

$counter = countUpTo(5);

foreach ($counter as $number) {
    echo $number . "\n";  // Outputs 1, 2, 3, 4, 5 one at a time
}


Breakdown:

	The countUpTo function is a generator. It starts from 1 and yields the number until it reaches the maximum value ($max).

	When the foreach loop iterates over $counter, the generator's yield pauses the function and returns the current value.

	After each iteration, the generator picks up where it left off, without re-executing the entire function.

Advantages of Using Generators:

	Memory Efficiency: Since they don’t store all the values in memory, generators are useful for working with large datasets (like reading from large files or processing large ranges).

	Performance: Generators only calculate the next value when needed, reducing unnecessary computation.

	Simplicity: They provide a clean, easy-to-understand way to work with iterators and sequences.

Regular function:

function getNumbers($max) {
    $numbers = [];
    for ($i = 1; $i <= $max; $i++) {
        $numbers[] = $i;
    }
    return $numbers;
}

This function returns all the numbers at once and stores them in an array, which could consume a lot of memory for large $max values.

Generator function:

function generateNumbers($max) {
    for ($i = 1; $i <= $max; $i++) {
        yield $i;
    }
}

If we want it to return an array we need to:

$gen = generateNumbers(5);
$nums = iterator_to_array($gen);
print_r($nums);

Summary:

A generator is a function that can be paused and resumed, and it allows you to produce values one at a time on demand. This makes generators especially useful for handling large datasets or sequences efficiently without using up a lot of memory.

You can think of the generator yielding values and a function processing each yielded value as similar to a callback mechanism.
With each value, you can execute a piece of code (process it), and once you're done, the generator will yield the next value.
This behavior allows you to handle values one at a time, rather than dealing with everything at once, making it memory efficient and flexible for large datasets or complex processing.


Interactive shell in terminal

    php -a

    Allows us to run php code without saving to a file
    

# FFMPEG

Cropping an webm while keeping the alpha channel - what a pain

	ffmpeg -c:v libvpx-vp9 -i input.webm -vf "crop=width:height:starting_x:starting_y" output.webm so if we want o get the first 1020x1080 we run:

		ffmpeg -c:v libvpx-vp9 -i input.webm -vf "crop=1920:1080:0:0" output-1.webm


# Ubuntu server

Update system hostname ( for wireless connection )

    sudo hostnamectl set-hostname my-ubuntu-server


# AWS

    Costs

        Set budget 

        Set cost anomaly

    EC2 instance

        ssh ubuntu@15.134.209.145