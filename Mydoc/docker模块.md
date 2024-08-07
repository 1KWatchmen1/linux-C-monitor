- 容器：容器是利用namespace将文件系统、进程、网络、设备等资源进行隔离，利用cgroup对权限、cpu资源进行限制，最终让容器之间互不影响，容器无法影响宿主机。
1、命名空间是一种隔离资源的方法，它将一组系统资源的视图从一个进程中隔离出来，使得该进程以及其子进程拥有自己的独立资源集
常见linux命令空间：PID Namespace、Network Namespace、Mount Namespace、UTS、Namespace、IPC Namespace、User Namespace
2、control group技术
控制容器中进程对系统资源的消耗
是一种用于限制和隔离一个或一组进程对系统资源使用的机制，将一组进程组织在一个控制组中，为这个控制组分配特定的资源限制和优先级，确保容器在共享主机上合理利用系统资源，避免资源竞争和过度使用。
CPU、Memory、BlockI/o、Network、Device
通过将容器的进程放入适当的cgroup中，可以限制他们对各种系统资源的访问。这种限制和隔离使得容器可以在相对独立的环境中运行。
3.容器的整体流程
    1、命名空间隔离
    2、Cgroup隔离
4.docker的优势
    1、运行在容器内的程序，使用的是宿主机的硬件资源，效率高
    2、docker直接宿主机的系统内核，避免了虚拟机启动时的资源消耗，速度快
    3、启动时间快、高效部署和扩容 部署简单（可以让用户把一个应用程序从一个平台直接迁移到另一个平台）
    4、虚拟机安全性高，
5、docker基本组成
    1、客户端
    2、服务器
    3、仓库：镜像的集合存储地
    镜像是由一层层的文件系统构建而成的，每一层文件系统都是前一层文件系统的增量变化。
    容器是镜像的实例，是一个独立的运行环境。
6、docker运行流程
Docker在本机寻找镜像->若本机存在这个镜像->使用此镜像运行；
                    ->若本机不存在此镜像->去docker hub上下载 -> docker hub上可以找到，那就下载下来，去运行
                                                            ->docker hub上找不到，返回错误
7、docker常用命令
    1、帮助命令
        docker version
        docker info //显用于显示 docker 的系统级信息，比如内核，镜像数，容器数等
        docker 命令 --help  //帮助命令
    2、镜像命令
        docker images //查看本地主机上的所有镜像
        docker search 镜像名    //搜索某个镜像,这是在docker hub上搜索，而非本地
        docker pull 镜像名    //下载镜像
        docker rmi 镜像名/镜像id   //删除镜像
        docker tag 镜像id 命名容器  //为镜像id命名
        docker run mysql    //新建容器并启动,注意这里有很多参数要使用
        docker run -d 镜像名    //后台启动容器,启动后，往往此时去docker ps一下，发现容器已经停止，因为docker容器使用后台进行，必须要有一个前台进程，docker发现没有应用，机会自动停止
        exit    //从容器中退出到主机
        ctrl + P + Q    //容器不停止退出(要在虚拟机里，远程不行)
        docker ps   //查看所有正在运行的容器
        docker ps -a    //查看当前正在运行的容器和历史中运行过的容器
        docker rm 容器id//删除容器，注意容器id和镜像id不是一回事，不允许删除正在运行的容器，强制删除-f
        docker start 容器id //启动容器
        docker restart 容器id   //重启容器
        docker stop 容器id  //停止当前正在运行的容器
        docker kill 容器id  //强制停止当前容器  
        docker logs -f -t --tail 容器id   //查看日志
        docker top 容器id   //查看容器中进程id，一个容器中可能有多个进程
        docker inspect 容器id   //查查看 Docker 容器或镜像的详细元数据。该命令会返回一个 JSON 格式的对象，包含有关容器或镜像的所有详细信息。
        docker exec -it 容器id bashshell    //我们通常运行容器都是在后台，需要修改才能进入容器内部
        docker save -o 输出名字 镜像名  //将镜像保存为一个归档文件，可以传输或备份
        docker load -i 指定输入的路径   //从规定那个文件中加载docker镜像
        docker build -t 镜像名 dockerfile的路径  //根据dockerfile创建docker镜像




        