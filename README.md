# Unity MCP with Ollama Integration

Connect AI language models (via Ollama) to Unity Editor using Model Context Protocol (MCP).

## 🎯 What This Does

This project enables AI assistants to control Unity Editor directly through natural language commands. You can ask an AI to:
- Create and modify GameObjects
- Change materials and colors
- Manage scenes
- Add components
- And much more!

## 📋 Prerequisites

Before starting, make sure you have:

1. **Unity Editor** (2021.3 or later recommended)
2. **Python 3.12+** installed
3. **Conda** (Anaconda or Miniconda)
4. **Ollama** installed and running
5. **Git** for version control

## 🚀 Installation Guide

### Step 1: Install Ollama

1. Download and install Ollama from [ollama.ai](https://ollama.ai)
2. Pull the DeepSeek Coder model:
   ```bash
   ollama pull deepseek-coder:latest
   ```
3. Verify Ollama is running:
   ```bash
   ollama list
   ```

### Step 2: Set Up Python Environment

1. Create a new Conda environment:
   ```bash
   conda create -n unity-mcp python=3.12
   conda activate unity-mcp
   ```

2. Install required Python packages:
   ```bash
   pip install httpx mcp fastapi uvicorn
   ```

### Step 3: Install Unity MCP Package

1. Open your Unity project
2. Open Package Manager (Window → Package Manager)
3. Click the **+** button → Add package from git URL
4. Enter: `https://github.com/ZundamonnoVRChatkaisetu/unity-mcp-ollama.git`
5. Wait for installation to complete

### Step 4: Configure the MCP Server

1. Navigate to: `Library/PackageCache/com.zundamonnovrchat.unity-mcp-ollama@[version]/Python/`
2. Edit `local_config.json`:
   ```json
   {
     "unity_host": "localhost",
     "unity_port": 6400,
     "mcp_port": 6500,
     "ollama_model": "deepseek-coder:latest",
     "ollama_host": "localhost",
     "ollama_port": 11434
   }
   ```

3. Fix the FastMCP bug in `server.py`:
   - Open `server.py`
   - Find line with `FastMCP("Unity MCP Server", description=...)`
   - Remove the `description` parameter
   - Should look like: `mcp = FastMCP("Unity MCP Server")`

### Step 5: Start the Servers

1. **Start Unity Bridge** (in Unity Editor):
   - The Unity Bridge should start automatically when Unity opens
   - Check Console for "Unity Bridge listening on port 6400"

2. **Start Python MCP Server**:
   ```bash
   conda activate unity-mcp
   cd "Library/PackageCache/com.zundamonnovrchat.unity-mcp-ollama@[version]/Python/"
   python server.py
   ```

3. Verify connection in Unity Console - you should see connection messages

## 🎮 Usage Examples

Once everything is running, you can send commands to Unity through the MCP interface.

### Example Commands:
- "Create a red cube at position (0, 1, 0)"
- "Change the color of the sphere to blue"
- "Add a Rigidbody component to the player"
- "Create 10 random spheres in the scene"

## 📁 Project Structure

```
Unity_mcp_Ollama/
├── Assets/                    # Unity assets
├── Library/                   # Unity library (not in git)
├── PackageCache/             
│   └── unity-mcp-ollama/     # MCP package
│       └── Python/           # Python server files
├── .gitignore                # Git ignore rules
└── README.md                 # This file
```

## 🔧 Troubleshooting

### Unity Bridge Not Starting
- Check Unity Console for errors
- Verify port 6400 is not in use
- Restart Unity Editor

### Python Server Connection Failed
- Ensure Conda environment is activated
- Check if Ollama is running: `ollama list`
- Verify ports 6400 and 6500 are available
- Check `local_config.json` settings

### Ollama Model Not Found
- Pull the model: `ollama pull deepseek-coder:latest`
- Verify with: `ollama list`
- Check model name in `local_config.json`

### FastMCP Error
- Remove `description` parameter from `FastMCP()` initialization in `server.py`
- This is a known bug in the package

## 🤝 Contributing

Feel free to open issues or submit pull requests!

## 📝 License

This project uses the unity-mcp-ollama package. Check the original repository for license details.

## 🙏 Credits

- Original MCP package: [unity-mcp-ollama](https://github.com/ZundamonnoVRChatkaisetu/unity-mcp-ollama)
- Ollama: [ollama.ai](https://ollama.ai)
- Model Context Protocol: [MCP](https://modelcontextprotocol.io)

## 📧 Contact

For questions or support, open an issue on GitHub.

---

**Note:** Ollama models are not included in this repository due to their size. You must download them separately using the `ollama pull` command.
