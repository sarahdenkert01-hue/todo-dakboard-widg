# 🎯 To-Do List Widget - Setup Instructions
Follow these steps to get your own personal to-do list widget running!

![To-Do Widget Demo](https://img.shields.io/badge/status-ready%20to%20use-brightgreen)

⚠️ Important: This widget requires setup before it will work. Don't skip any steps! ⚠️

## ✨ Step 1: Create a free Supabase account

- Go to supabase.com
- Click "Start your project" and sign up (it's free!)
- Create a new organization (just use your name)
- Click "New Project"
- Give it a name like "my-todo-list"
- Create a database password (save this somewhere safe!)
- Choose a region close to you
- Click "Create new project" (takes 2-3 minutes)

## Step 2: Set up your database

- In your Supabase project, click "SQL Editor" in the left sidebar
- Click "New Query"
- Copy and paste this entire SQL code:

```html



    
-- Create lists table
CREATE TABLE lists (
  id bigint PRIMARY KEY GENERATED ALWAYS AS IDENTITY,
  name text NOT NULL,
  position int DEFAULT 0,
  x_position int DEFAULT 0,
  y_position int DEFAULT 0,
  created_at timestamp with time zone DEFAULT now()
);

-- Enable Row Level Security for lists
ALTER TABLE lists ENABLE ROW LEVEL SECURITY;

-- Create policy to allow all operations on lists
CREATE POLICY "Enable all access for lists"
ON lists
FOR ALL
USING (true)
WITH CHECK (true);

-- Update tasks table to use bigint for list_id
ALTER TABLE tasks ALTER COLUMN list_id TYPE bigint USING list_id::bigint;

ALTER TABLE lists ADD COLUMN width int DEFAULT 250;
    


    


```
- Click "Run" at the bottom right
- You should see "Success. No rows returned"
  
## Step 3: Enable real-time updates

- Click "Database" in the left sidebar
- Click "Replication"
- Find the "tasks" table and toggle it ON
- Find the "lists" table and toggle it ON
- Click "Save"

## Step 4: Get your API credentials

- Click the gear icon ⚙️ (Project Settings) in the left sidebar
- Click "API"
- You'll see two important things:
- Project URL - looks like: https://xxxxx.supabase.co
- anon/public key - a long string starting with "eyJ..."
- Keep this tab open - you'll need these in the next step!

## Step 5: Update your HTML files
You need to add your credentials to BOTH index.html and mobile.html files:

- Open index.html in a text editor
- Find these lines near the top of the <script> section:

  const SUPABASE_URL = 'YOUR_SUPABASE_URL_HERE';
  const SUPABASE_KEY = 'YOUR_SUPABASE_ANON_KEY_HERE';

- Replace them with your actual credentials (keep the quotes!):

  const SUPABASE_URL = 'https://xxxxx.supabase.co';
  const SUPABASE_KEY = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...';

- Save the file
- Repeat steps 1-4 for mobile.html

## Step 6: Host your widget

- Create a GitHub account at github.com
- Create a new repository (name it something like "my-todo-widget")
- Upload both HTML files (index.html and mobile.html)
- Go to Settings → Pages
- Under "Source", select "main" branch
- Click Save
- Your widget will be at: https://your-username.github.io/my-todo-widget/

### On DakBoard:
1. Add a **Widget** block
2. Copy and paste the following:
   
```html



    
    
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <style>
        body, html {
            margin: 0;
            padding: 0;
            width: 100%;
            height: 100%;
            overflow: hidden;
            background: transparent;
        }
        iframe {
            width: 100%;
            height: 100%;
            border: none;
            background: transparent;
        }
    </style>
</head>
<body>
    <iframe src="INSERT GITHUB PAGE URL" allowtransparency="true" frameborder="0" scrolling="no"></iframe>
</body>
</html>
    


    


```
3. Replace `INSERT_YOUR_GITHUB_PAGES_URL_HERE` with your actual URL: `https://your-username.github.io/your-repo/`
4. Save the block
5. Resize and position on your dashboard
6. Drag lists to arrange them as you like
7. Resize lists by dragging their right edge

### On Your Phone:
1. Open the mobile version: `https://your-username.github.io/your-repo/mobile.html`
2. Add to home screen for easy access:
   - **iPhone:** Safari → Share → Add to Home Screen
   - **Android:** Chrome → Menu → Add to Home Screen
3. All changes sync instantly with your DakBoard!

## 🎨 Customization

You can customize:
- **Colors:** Edit the CSS gradients and backgrounds
- **Font:** Change `font-family: 'Comfortaa'` to any Google Font
- **Sizes:** Adjust font sizes, padding, and spacing in the CSS
- **Layout:** Lists can be positioned anywhere on DakBoard

## 🔒 Privacy & Data

- Your data is stored in YOUR Supabase database (not shared with anyone)
- Only people with your GitHub Pages URL can access your widget
- Don't share your Supabase credentials with anyone
- Want to collaborate? Just share your URL with family/friends!

## 🐛 Troubleshooting

**Widget shows "Loading..." forever:**
- Check that you added your Supabase credentials to BOTH files
- Make sure you ran the SQL setup script
- Open browser console (F12) to see error messages

**Tasks don't sync:**
- Enable Replication for both tables in Supabase (see setup guide)
- Make sure all devices use the same URL

**Can't add lists:**
- Verify you created BOTH the tasks and lists tables
- Check browser console for errors

For more help, see the troubleshooting section in `SETUP_INSTRUCTIONS.html`


## 📝 License

Free to use and modify for personal use. Share it, customize it, make it your own!

## 🆘 Need More Help?

1. First, check `SETUP_INSTRUCTIONS.html` - it has detailed steps with code examples
2. Open your browser console (F12) to see error messages
3. Make sure you completed ALL setup steps, especially:
   - Running the SQL script
   - Enabling Replication
   - Adding credentials to BOTH HTML files
