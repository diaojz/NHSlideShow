# NHSlideShow
This control provides varity of animation options to run a slideshow on iphone, ipod and ipad as well. It maintains a circular queue of images.

This control is also available on Cocoacontrols.com:
https://www.cocoacontrols.com/controls/nhslideshow

Here is how it looks like:

<img src="https://journeytoios.files.wordpress.com/2015/01/screen-shot.png" alt="Runtime View">

The attached source code is available for both storyboard and XIBs. On slight modification in code can change the mode from storyboard to XIBs.

<strong>How to integrate:</strong>

<pre>

- (void)viewDidLoad
{
     [super viewDidLoad];

      // Create slide show control
      slideShow = [[NHSlideShow alloc] initWithFrame:CGRectMake(0, 0, kScreenSize.height, kScreenSize.width)]; 
     [slideShow setDelayInTransition:2.0f];
     [slideShow setDelegate:self];
     [slideShow slidesWithImages:[self getImages]];
}

-(void)viewDidLayoutSubviews
{
    [super viewDidLayoutSubviews];
    
     // This will help to run the same code on iphone if single layout files 
     // designed for both iphone 4 and iphone 5.
    [slideShow doneLayout];
    
     // Start slide show
    [slideShow start];
}

#pragma mark - Helper functions

-(NSArray *)getImages
{
    // Create array of images to be run in slide show
     NSMutableArray *mArr = [[NSMutableArray alloc] init];
    
    [mArr addObject:[UIImage imageNamed:@"1.png"]];
    [mArr addObject:[UIImage imageNamed:@"2.png"]];
    [mArr addObject:[UIImage imageNamed:@"3.png"]];
    
    [mArr addObject:[UIImage imageNamed:@"4.png"]];
    [mArr addObject:[UIImage imageNamed:@"5.png"]];
    [mArr addObject:[UIImage imageNamed:@"6.png"]];
    
    [mArr addObject:[UIImage imageNamed:@"7.png"]];
    [mArr addObject:[UIImage imageNamed:@"8.png"]];
    [mArr addObject:[UIImage imageNamed:@"9.png"]];
    
    [mArr addObject:[UIImage imageNamed:@"10.png"]];    
    
     return mArr;
}

#pragma mark - Event Handlers

-(IBAction)valueChanged:(UISegmentedControl *)segmentedControl
{
    // Change animation mode
    NSLog(@"ValueChanged...");
    
    switch (segmentedControl.selectedSegmentIndex)
    {
        case NHSlideShowModeSwipeLeft:
        {
            [slideShow setSlideShowMode:NHSlideShowModeSwipeLeft];
        }break;
        case NHSlideShowModeFade:
        {
            [slideShow setSlideShowMode:NHSlideShowModeFade];
        }break;
        case NHSlideShowModeScale:
        {
            [slideShow setSlideShowMode:NHSlideShowModeScale];
        }break;
        case NHSlideShowModeWindow:
        {
            [slideShow setSlideShowMode:NHSlideShowModeWindow];
        }break;
        case NHSlideShowModeRandom:
        {
            [slideShow setSlideShowMode:NHSlideShowModeRandom];
        }break;
        default:
            break;
    }  
}

-(IBAction)modeValueChanged:(UISegmentedControl *)segmentedControl
{
    // Change slide execution mode
    NSLog(@"ValueChanged...");
    
    switch (segmentedControl.selectedSegmentIndex)
    {
        case 0:
        {
            [slideShow start];
        }break;
        case 1:
        {
            [slideShow stop];
        }break;
        default:
            break;
    }
}

-(IBAction)btnNext_Click:(id)sender
{
     // Move to next slide
    [slideShow moveNext];
}

-(IBAction)btnPrevious_Click:(id)sender
{
     // Move to previous slide
    [slideShow movePrevious];
}

#pragma mark - NHSlideShow delegate functions


-(NSInteger)slideShowShouldStartFromSlide:(NHSlideShow *)slideShow
{
    return 0; // Return your starting slide number
}

-(void)slideShow:(NHSlideShow *)slideShow didChangedSlideAtIndex:(NSInteger)slideIndex
{
    // TODO: You can display your image description using this delegate.
    NSLog(@"didChangedSlideAtIndex : %ld", (long)slideIndex);
}
</pre>
