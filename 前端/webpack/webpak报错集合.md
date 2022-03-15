# webpak报错集合

## less

##### 1.注释处报告单词错误

**如图:**

![1646722660520](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\1646722660520.png)

**解决办法**：

我的样式处理配置是

```json
//设置less文件的处理
{
    test: /\.less$/,
    use: [
        "style-loader",
        "css-loader",
        "less-loader",
        {
            loader: 'postcss-loader',
            options: {
                postcssOptions: {
                    plugins: [
                        [
                            "postcss-preset-env", {
                                browsers: 'last 2 versions'
                            }
                        ]
                    ]
                }
            }
        },
    ]
}
```

加载器位置出错，应层层迭代，由style-loader处理经过css-loader再通过postcss-loader处理语法，最后less-loader。如图

```json
//设置less文件的处理
{
    test: /\.less$/,
    use: [
        "style-loader",
        "css-loader",
        {
            loader: 'postcss-loader',
            options: {
                postcssOptions: {
                    plugins: [
                        [
                            "postcss-preset-env", {
                                browsers: 'last 2 versions'
                            }
                        ]
                    ]
                }
            }
        },
        "less-loader",
    ]
}
```

