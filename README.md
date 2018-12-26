# ˵��
΢������Ŀʾ����

## ʹ�÷���

```csharp
// Startup.cs
public void ConfigureServices(IServiceCollection services)
        {
services.AddMicroService(new MicroserviceOptions()
            {
                MicroServiceName = "apiresource",

                AssemblyName = Assembly.GetExecutingAssembly().GetName().Name,

                Scopes = typeof(ClientScopes),

                Permissions = typeof(UserPermissions)
            });
                //...
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

            app.UseStaticFiles();

            app.UseMicroservice();

            app.UseMvc();
        }
```


#### ��Ҫ���ԣ��Զ���Ȩ�ޡ������ԡ���汾�����/����ͳһ��ʽ��

![swagger](swagger.png)

#### ����������

    ����Resources/Controllers�ṹ��Ӽ���,���Ʊ�����controller��Ӧ

#### ΢�������ã���MicroserviceConfig.cs�ļ���

  * ClientȨ�޶��壺ClientScopes Class

  * UserȨ�޶��壺UserPermissions Class

#### �������ã�appsettings.json��
    * IdentityServer��
        identityserver4��Ȩ���ĵķ�������ַ���磺ids.ixingban.com

#### ���ݿ�����

```text
The generated database code requires Entity Framework Core Migrations. Run the following commands:
1. dotnet ef migrations add CreateDbSchema
2. dotnet ef database update
 Or from the Visual Studio Package Manager Console:
1. Add-Migration CreateIdentitySchema
2. Update-Database
```

#### ��Ʋο��ĵ�
  
  - https://docs.microsoft.com/zh-cn/azure/architecture/best-practices/api-design
  
  - https://github.com/Microsoft/api-guidelines/blob/master/Guidelines.md
  
  - http://restcookbook.com/
  
  - https://mathieu.fenniak.net/the-api-checklist/
  
  - https://docs.microsoft.com/zh-cn/azure/architecture/best-practices/api-implementation#more-information