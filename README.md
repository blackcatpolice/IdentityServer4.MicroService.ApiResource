# ˵��
΢������Ŀʾ����

## ʹ�÷���

```csharp
// Startup.cs
        // This method gets called by the runtime. Use this method to add services to the container.
        public void ConfigureServices(IServiceCollection services)
        {
            services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_2);

            services.AddMicroService(Configuration, options => {

                // �Ǳ����������þͲ�������API��Ȩ
                options.IdentityServerUri = new Uri("IdentityServer4��������ַ");

                // ������д
                options.MicroServiceRedirectUrls = new List<string>()
                {
                    "https://{��ǰ��Ŀ��ַ}/swagger/oauth2-redirect.html"
                };

                // �Ǳ���
                //options.MicroServiceName = Assembly.GetExecutingAssembly().GetName().Name;
                //options.MicroServiceDisplayName = "MicroServiceDisplayName";
                //options.MicroServiceDescription = "MicroServiceDescription";
                //options.MicroServiceClientIDs = new List<string>() { "swagger" };
                //options.EnableApiVersioning = true;
                //options.EnableAuthorizationPolicy = true;
                //options.EnableCors = true;
                //options.EnableLocalization = true;
                //options.EnableResponseCaching = true;
                //options.EnableSwaggerGen = true;
                //options.EnableSwaggerUI = true;
                //options.EnableWebEncoders = true;
                //options.ImportToIdentityServer = true;
            });
        }


       // This method gets called by the runtime. Use this method to configure the HTTP request pipeline.
        public void Configure(IApplicationBuilder app, IHostingEnvironment env)
        {
            if (env.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();
            }
            else
            {
                // The default HSTS value is 30 days. You may want to change this for production scenarios, see https://aka.ms/aspnetcore-hsts.
                app.UseHsts();
            }

            app.UseHttpsRedirection();

            app.UseMicroservice();

            app.UseMvc();
        }
```


#### ��Ҫ���ԣ��Զ���Ȩ�ޡ������ԡ���汾�����/����ͳһ��ʽ��

![swagger](swagger.png)

#### ����������

    ����Resources/Controllers�ṹ��Ӽ���,���Ʊ�����controller��Ӧ

#### APIȨ������
```csharp
// GET api/values
        [HttpGet]
        // ��֤clientȨ��
        // ע���ʽ����scope:{��ǰcontroller����Сд}.Ȩ������
        [Authorize(Policy = "scope:values.get")]
        // ��֤�û�Ȩ��
        // ע���ʽ����permission:{��ǰcontroller����Сд}.Ȩ������
        [Authorize(Policy = "permission:values.get")]
        // �ӿ�����
         // ע���ʽ��controller����+action����
        [SwaggerOperation(OperationId = "ValuesGet")]
        public ActionResult<IEnumerable<string>> Get()
        {
            return new string[] { "value1", "value2" };
        }
```

#### appsettings.json����
΢����ģʽ����API���ӵ�IdentityServer4������appsettings.json�ļ�
```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Warning"
    }
  },
  "AllowedHosts": "*",
  "MicroService": {
    "IdentityServer": "IdentityServer4��ַ",
    "Name": "apiresource",
    "DisplayName": "΢����",
    "Description": "΢���������Ŀ",
    "ClientIDs": [ "swagger" ],
    "RedirectUrls": [ "https://��ǰ��Ŀ��ַ/swagger/oauth2-redirect.html" ]
  }
}

#### ��Ʋο��ĵ�
  
  - https://docs.microsoft.com/zh-cn/azure/architecture/best-practices/api-design
  
  - https://github.com/Microsoft/api-guidelines/blob/master/Guidelines.md
  
  - http://restcookbook.com/
  
  - https://mathieu.fenniak.net/the-api-checklist/
  
  - https://docs.microsoft.com/zh-cn/azure/architecture/best-practices/api-implementation#more-information