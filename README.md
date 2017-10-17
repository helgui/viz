# OpenCV Viz
Modified OpenCV Viz module with access to VTK backend. It provides three new public methods of Viz3d:
```c++
void* getVtkRenderer();
void* getVtkInteractor();
void* getVtkRenderWindow();
```
Example:
```c++
//Z-Buffer acquisition
cv::viz::Viz3d viz3d;
//...
cv::Size ws = viz3d.getCamera().getWindowSize();
vtkRenderWindow *renderWindow = (vtkRenderWindow*)viz3d.getVtkRenderWindow();
vtkSmartPointer<vtkFloatArray> zBufferRaw = vtkSmartPointer<vtkFloatArray>::New();
zBufferRaw->SetNumberOfComponents(1);
zBufferRaw->SetNumberOfValues(ws.area());
renderWindow->GetZbufferData(0, 0, ws.width - 1, ws.height - 1, zBufferRaw);
cv::Mat depth(ws, CV_32F, zBufferRaw->GetPointer(0));
//...
```
