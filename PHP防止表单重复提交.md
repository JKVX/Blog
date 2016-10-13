	**【问题】**
	表单提交后跳转到新页面，当进行页面刷新时，表单会重复提交，这时候会造成错误。如提交表单后执行插入操作的类型，会重复插入数据；如A页面提交表单后跳转到新页面B，再次点击按钮跳转到页面C，这时候点击浏览器的后退/返回按钮想返回页面B会出错，提示信息丢失等，因为返回到页面B时，原先的表单提交内容已经丢失。
	**【解决方案】**
	*方案一：*在表单提交到后台的函数D中进行处理并执行跳转页面的操作，将原先该跳转操作的代码段放到一个新的函数E中，然后执行redirect(url)函数,其中url为函数E的url地址。该方法就避免了表单的重复提交，因为url地址不再是原先的函数D的url地址，而变成了函数E的url地址，刷新后，执行的后台函数是函数E。
	

```
//原先的函数
    public function admin($role){
        switch ($role) {
            case 1:
            case 2:
                $this->load->view('templates/header');
		        $this->load->view('home/home_admin');
                break;
            case 3:
            case 4:
                $this->load->view('templates/header');
		        $this->load->view('research/research_admin');
                break;
        }
    }
//修改后的函数
    public function admin($role){
        switch ($role) {
            case 1:
            case 2:
                redirect(site_url('home/home_admin'));
                break;
            case 3:
            case 4:
                redirect(site_url('research/research_admin'));
                break;
        }
    }
    public function research_admin(){
        $this->load->view('templates/header');
        $this->load->view('research/research_admin');
    }
    public function home_admin(){
        $this->load->view('templates/header');
        $this->load->view('home/home_admin');
    }

```