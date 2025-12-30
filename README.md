# 12306购票搜索服务器 

基于 Model Context Protocol (MCP) 的12306购票搜索服务器。提供了简单的API接口，允许大模型利用接口搜索12306购票信息。
12306 ticket purchase search server based on Model Context Protocol (MCP). It provides a simple API interface, allowing large models to search for 12306 ticket purchasing information through the interface.## 工具列表 Tool List

本MCP服务封装下列工具，可让模型通过标准化接口调用以下功能。 本MCP服务封装下列工具，可让模型通过标准化接口调用以下功能。

| 工具 Tool   | 描述 Description         |
|-------|--------------------|
| get-current-date | 获取当前日期，以上海时区（Asia/Shanghai, UTC+8）为准，返回格式为 "yyyy-MM-dd"。主要用于解析用户提到的相对日期（如“明天”、“下周三”），提供准确的日期输入。 |
| get-stations-code-in-city | 通过中文城市名查询该城市 **所有** 火车站的名称及其对应的 `station_code`，结果是一个包含多个车站信息的列表。 |
| get-station-code-of-citys | 通过中文城市名查询代表该城市的 `station_code`。此接口主要用于在用户提供**城市名**作为出发地或到达地时，为接口准备 `station_code` 参数。 |
| get-station-code-by-names | 通过具体的中文车站名查询其 `station_code` 和车站名。此接口主要用于在用户提供**具体车站名**作为出发地或到达地时，为接口准备 `station_code` 参数。 |
| get-station-by-telecode | 通过车站的 `station_telecode` 查询车站的详细信息，包括名称、拼音、所属城市等。此接口主要用于在已知 `telecode` 的情况下获取更完整的车站数据，或用于特殊查询及调试目的。一般用户对话流程中较少直接触发。 |
| get-tickets | 查询12306余票信息。 |
| get-interline-tickets | 查询12306中转余票信息。尚且只支持查询前十条。 |
| get-train-route-stations | 查询特定列车车次在指定区间内的途径车站、到站时间、出发时间及停留时间等详细经停信息。当用户询问某趟具体列车的经停站时使用此接口。 |


## 检查服务 ## Inspector

工具在线测试： [https://mcp.xiaobenyang.com/inspector/1777316659202051](https://mcp.xiaobenyang.com/inspector/1777316659202051)

Online Tool test [https://mcp.xiaobenyang.com/inspector/1777316659202051](https://mcp.xiaobenyang.com/inspector/1777316659202051)

## 服务配置 MCP Server Config


> #### 如何获取 XBY-APIKEY ？ How to get XBY-APIKEY ?
> 访问小笨羊科技网站 [https://xiaobenyang.com](https://xiaobenyang.com)，注册用户即可获得APIKEY
> Visit XiaoBenYang website [https://xiaobenyang.com](https://xiaobenyang.com), register and get the APIKEY.

### SSE
```json
{
  "mcpServers": {
    "12306购票搜索服务器": {
      "headers": {
        "XBY-APIKEY": "<YOUR_XBY_APIKEY>"
      },
      "type": "sse",
      "url": "https://mcp.xiaobenyang.com/1777316659202051/sse"
    }
  }
}
```
### STREAMABLE HTTP
```json
{
  "mcpServers": {
    "12306购票搜索服务器": {
      "headers": {
        "XBY-APIKEY": "<YOUR_XBY_APIKEY>"
      },
      "type": "streamable_http",
      "url": "https://mcp.xiaobenyang.com/1777316659202051/mcp"
    }
  }
}
```
### STDIO
```json
{
    "mcpServers": {
        "12306购票搜索服务器": {
          "command": "npx",
          "args": [
            "-y",
            "xiaobenyang-mcp"
          ],
          "env": {
            "XBY_APIKEY": "<YOUR_XBY_APIKEY>",
            "mcpId": "1777316659202051",
          },
          "transport": "stdio"
        }
      }
}

```
