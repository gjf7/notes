# overview
1. QT main -> Application -> app -> launch_services(image_decoder and request_server)-> new_window -> BrowserWindow -> new_tab_from_url -> create_new_tab -> new Tab(this) -> WebContentView -> initialize_client

2. initialize_client

```c++
auto request_server_socket = connect_new_request_server_client()
auto image_decoder_socket = connect_new_image_decoder_client()

m_client_state.client = launch_web_content_process()
```

3. launch_web_content_process
setup arguments and launch WebContent
```c++
return launch_server_process<WebView::WebContentClient>("WebContent"sv, move(arguments), view);

// launch_server_process


auto result = WebView::Process::spawn<ClientType>(process_type, move(options), forward<ClientArguments>(client_arguments)...);


auto&& [process, client] = result.release_value();

if constexpr (requires { client->set_pid(pid_t {}); })
    client->set_pid(process.pid());

WebView::Application::the().add_child_process(move(process));

return client;
```
